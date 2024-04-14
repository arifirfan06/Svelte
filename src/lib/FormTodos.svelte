<script>
import { createEventDispatcher } from "svelte";
export let disableAdd
const dispatch = createEventDispatcher()

let input = ''

export function clearInput() {
    input = ''
}

function submitHandler() {
    if(!input) return;
    console.log(input)
    dispatch('todo', {title: input})
}

</script>

<form class="add-todos" on:submit|preventDefault={submitHandler}>
  <input bind:value={input} type="text" />
  <button disabled={disableAdd}>Submit</button>
</form>

<style>
</style>
