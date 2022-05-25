<script>
  import {
    Header,
    HeaderActionLink,
    HeaderUtilities,
  } from "carbon-components-svelte";
  import LogoGithub from "carbon-icons-svelte/lib/LogoGithub.svelte";
  import "carbon-components-svelte/css/g100.css";
</script>

<svelte:head>
  <title>CodeFly: Share your code easily</title>
</svelte:head>

<Header company="Code" platformName="Fly" href="/">
  <HeaderUtilities>
    <HeaderActionLink
      icon={LogoGithub}
      href="https://github.com/hisamafahri/codefly"
      target="_blank"
    />
  </HeaderUtilities>
</Header>

<slot />
