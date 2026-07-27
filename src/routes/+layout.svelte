<script lang="ts">
  import "./layout.css";
  import favicon from "$lib/assets/favicon.svg";

  let { children } = $props();
</script>

<svelte:head
  ><meta
    name="viewport"
    content="width=device-width, initial-scale=1.0 viewport-fit=cover"
  /><link rel="icon" href={favicon} /></svelte:head
>
<title>Welcome to elc.moe!</title>
{@render children()}
