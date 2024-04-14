<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  export let shadow = false;
  export let size = "small";
  export let textColor = null;
  export let bgColor = null;
  let clicked = false;
  console.log($$slots);
</script>

<!-- in svelte have directed to manage dynamic css class -->
<!-- we can also make style directive instead of style="background-color: {bgColor}; color: {textColor}" -->
<!-- we can simply use on:click to foward child to parent in button -->
<button
  {...$$restProps}
  style:--btnBgColor={bgColor}
  style:color={textColor}
  class:shadow
  class:size-lg={size === "large"}
  class:size-md={size === "medium"}
  on:click={() => dispatch("click1", { message: "test wow" })}
>
  {#if $$slots.icon}
    <div class="icon">
      <slot name="icon" />
    </div>
  {/if}
  <!-- slot props child -> parrent component -->
  <slot {clicked} /></button
>

<!-- <button
  style:--btnBgColor={bgColor}
  style:color={textColor}
  class:shadow
  class:size-lg={size === "large"}
  class:size-md={size === "medium"}
  on:click={() => clicked = !clicked}
> -->

<!-- add falback / default value in slot -->
<!-- <button><slot>BUTTON</slot></button> -->

<style lang="scss">
  @use "../assets/btn.scss";

  button {
    display: flex;
    align-items: center;
    border: none;
    background-color: var(--btnBgColor);
    color: var(--btnTextColor);
    border-radius: 7px;
    padding: 10px;
    .icon {
      margin-right: 10px;
    }
    &:hover {
      background-color: rgb(113, 200, 84);
      color: btn.$color;
    }
    &:active {
      color: rgb(19, 116, 200);
    }
    &.size-md {
      padding: 20px;
    }
    &.size-lg {
      padding: 30px;
    }
    &.shadow {
      box-shadow: 0 0 10px #4d5959;
    }
  }
</style>
