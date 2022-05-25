<script>
  import {
    Header,
    Content,
    Grid,
    Row,
    Column,
    HeaderUtilities,
    HeaderActionLink,
  } from "carbon-components-svelte";
   import LogoGithub from "carbon-icons-svelte/lib/LogoGithub.svelte";
</script>

<svelte:head>
    <title>CodeFly: Share your code easily</title>
</svelte:head>

<Header company="Code" platformName="Fly" href="/">
  <HeaderUtilities>
    <HeaderActionLink
        icon="{LogoGithub}"
        href="https://github.com/hisamafahri/codefly"
        target="_blank"
    />
  </HeaderUtilities>
</Header>

<Content>
  <Grid>
    <Row>
      <Column>
        <h1>Welcome to CodeFly</h1>
      </Column>
    </Row>
  </Grid>
</Content>

