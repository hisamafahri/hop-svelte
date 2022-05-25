<script>
  import {
    Content,
    Grid,
    Column,
    TextArea,
  } from "carbon-components-svelte";
</script>

<Content>
  <Grid>
    <Column>
      <h1 style={"margin-bottom: 24px;"}>Let Your Codes Fly</h1>
      <TextArea
        labelText="Code Desription"
        placeholder="Enter your code description..."
        maxCount={512}
      />
    </Column>
  </Grid>
</Content>
