<script lang="ts">
  import {
    Content,
    Grid,
    Column,
    TextArea,
    Button,
    Row,
    Tabs,
    Tab,
    TabContent,
    Modal,
    TextInput,
  } from "carbon-components-svelte";
  import { ArrowRight } from "carbon-icons-svelte";
  import type monaco from "monaco-editor";
  import { onMount } from "svelte";

  import editorWorker from "monaco-editor/esm/vs/editor/editor.worker?worker";
  import jsonWorker from "monaco-editor/esm/vs/language/json/json.worker?worker";
  import cssWorker from "monaco-editor/esm/vs/language/css/css.worker?worker";
  import htmlWorker from "monaco-editor/esm/vs/language/html/html.worker?worker";
  import tsWorker from "monaco-editor/esm/vs/language/typescript/ts.worker?worker";

  // @ts-ignore
  let divEl: HTMLDivElement = null;
  let editor: monaco.editor.IStandaloneCodeEditor;
  let Monaco;

  onMount(async () => {
    // @ts-ignore
    self.MonacoEnvironment = {
      getWorker: function (_moduleId: any, label: string) {
        if (label === "json") {
          return new jsonWorker();
        }
        if (label === "css" || label === "scss" || label === "less") {
          return new cssWorker();
        }
        if (label === "html" || label === "handlebars" || label === "razor") {
          return new htmlWorker();
        }
        if (label === "typescript" || label === "javascript") {
          return new tsWorker();
        }
        return new editorWorker();
      },
    };

    Monaco = await import("monaco-editor");
    editor = Monaco.editor.create(divEl, {
      language: "javascript", // TODO: Make it dynamic
      value: "",
      theme: "vs-dark",
    });

    return () => {
      editor.dispose();
    };
  });
  let open = false;
  let defaultFileName = "Untitled";
  let fileName = defaultFileName;
</script>

<Content>
  <Grid>
    <Row>
      <Column>
        <h1 style="margin-bottom: 16px;">Let Your Codes Fly 🚀</h1>
        <p style="margin-bottom: 36px;">
          Share your codes with your friends, collagues, or anyone easily, for
          free!
        </p>
        <TextArea
          labelText="Code Desription"
          placeholder="Enter your code description..."
          maxCount={1024}
        />
        <div
          style="align-self:stretch; display: flex; align-items: center; justify-content: flex-end; margin-top: 24px; margin-bottom: 24px;"
        >
          <Button icon={ArrowRight}>Get Shareable Link</Button>
        </div>
      </Column>
      <Column>
        <Tabs type="container" style="padding: 0;">
        <div on:dblclick={() => (open = true)}>
            <Tab label={fileName} />
          </div>
          <svelte:fragment slot="content">
            <TabContent style="padding: 0px; height: 80vh; overflow: hidden">
              <div bind:this={divEl} style="height: 100%;" />
            </TabContent>
          </svelte:fragment>
        </Tabs>
      </Column>
    </Row>
  </Grid>
</Content>

<!-- Change file name modal -->
<Modal
  bind:open
  modalHeading="Change File Name"
  primaryButtonText="Save"
  secondaryButtonText="Cancel"
  on:click:button--secondary={() => (open = false)}
  on:click:button--primary={() => (open = false, fileName = defaultFileName)}
  on:open
  on:close
  on:submit
>
  <TextInput
    labelText="File Name"
    placeholder="Enter file name..."
    bind:value={defaultFileName}
  />
</Modal>
