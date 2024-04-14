<script>
  import Button from "./lib/Button.svelte";
</script>

<!-- simple props child to parrent access on:click={() => alert('test')} -->
<Button
  on:click1={(e) => alert(e.detail.message)}
  let:clicked
  bgColor={"black"}
  textColor={"white"}
  shadow
  size={"medium"}
  >CLICK ME
  <!-- {leftHovered} -->
  {#if clicked}
    ??
  {:else}
    Good
  {/if}
  <span slot="icon">{"><"}</span>
</Button>

<style>
</style>
