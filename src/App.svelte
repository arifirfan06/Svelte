<script>
  import FormTodos from "./lib/FormTodos.svelte";
  import ToDolist from "./lib/ToDolist.svelte";
  import { v4 as uuid } from "uuid";
  // tick is asyncronus it make sure dom is updated before proceed to next function
  import { tick } from "svelte";
  let formToDos;
  let isAdding = false
  let todos = [];

  async function updateTodo(e) {
    isAdding = true
    await fetch("https://jsonplaceholder.typicode.com/todos", {
      method: "POST",
      body: JSON.stringify({ title: e.detail.title, completed: false }),
      headers: {
        'Content-type': 'application/json'
      }
    }).then(async (response) => {
      if (response.ok) {
        // return (todos = await response.json());
        const item = await response.json()
        todos = [...todos, { ...item, id: uuid()}];
      } else {
        throw new Error("Error found while fetching todos");
      }
    });
    isAdding = false
    // console.log(todos)
    // await tick();
    // console.log(document.querySelectorAll(".item-todo"));
    formToDos.clearInput();
  }
  async function removeHandler(e) {
    await fetch(`https://jsonplaceholder.typicode.com/todos/${e.detail.id}`, {
      method: "DELETE",
      headers: {
        'Content-type': 'application/json'
      }
    }).then(async (response) => {
      if (response.ok) {
        todos = todos.filter((item) => item.id !== e.detail.id);
      } else {
        throw new Error("Error found while fetching todos");
      }
    });
  }

  function loadToDo() {
    fetch("https://jsonplaceholder.typicode.com/todos?_limit=7").then(
      async (response) => {
        if (response.ok) {
          return (todos = await response.json());
        } else {
          throw new Error("Error found while fetching todos");
        }
      }
    );
  }

  async function checkHandler(e) {
    await fetch(`https://jsonplaceholder.typicode.com/todos/${e.detail.id}`, {
      method: "PATCH",
      body: JSON.stringify({completed: e.detail.completed}),
      headers: {
        'Content-type': 'application/json'
      }
    }).then(async (response) => {
      if (response.ok) {
       const updatedCheck = await response.json()
        todos = todos.map((item) => {
      if (item.id === e.detail.id) {
        return updatedCheck
      }
      return item;
    });
      } else {
        throw new Error("Error found while fetching todos");
      }
    });
  }

  loadToDo();
</script>

<!-- {#await loadToDo()} -->
<!-- {:then} {:catch error} -->
<!-- {(console.log(todos), '')} -->
<ToDolist on:check={checkHandler} on:remove={removeHandler} {todos} />
<!-- {/await} -->
<FormTodos bind:this={formToDos} disableAdd={isAdding} on:todo={updateTodo} />

<style>
</style>
