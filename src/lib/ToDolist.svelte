<script>
  import { createEventDispatcher, onDestroy, onMount } from "svelte";
  import { beforeUpdate, afterUpdate } from "svelte";
  export let todos = [];  

  // onMount(() => {
  //   // run once when component mounted. use it on top level of script
  //   console.log('mounted')
  //   return () => {
  //     console.log('destroyed')
  //   }
  // })

  // onDestroy(() => {
  //   // when component unmount
  //   console.log('onDestroy')
  // })

  // beforeUpdate(()=> {
  //   console.log('beforeUpdate')
  // })

  // afterUpdate(() => {
  //   console.log('afterUpdate')
  // })

  const dispatch = createEventDispatcher();
  function removeClick(item) {
    // console.log('picked', item)
    dispatch("remove", item);
  }

  function checkClick(todo, e) {
    // console.log(e.currentTarget.checked, todo);
    const updatedComplete = {
      title: todo.title,
      id: todo.id,
      completed: e.currentTarget.checked,
    };

    dispatch("check", updatedComplete);
  }
</script>

<!-- we can also destructure and assign id each loop with -->
<!-- {#each todos as {title, id}, index (id)} -->
{#each todos as todo, index (todo.id)}
<!-- debugging consolelog via html tag with (() => {}, '') it run on terminal but return nothing or ''-->
<!-- {(console.log(todo), '')} -->
<!-- this will trigger log and debug in browser add breakpoint it also stop code execution -->
<!-- {@debug todo} -->
  {@const number = index + 1}
  <li class="item-todo">
    <label>
      <input
        on:input={(e) => checkClick(todo, e)}
        type="checkbox"
        checked={todo.completed}
      />
      {number} - {todo.title}
    </label>
    <button style="margin: 7px" on:click={() => removeClick(todo)}
      >Remove</button
    >
  </li>
{/each}

<style>
</style>
