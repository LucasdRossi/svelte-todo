<script lang="ts">
  interface Todos {
    id: number;
    text: string;
    completed: boolean;
  }

  let newTodoText = "";
  let todos: Todos[] = [
    {
      completed: false,
      id: 0,
      text: "Learn Svelte",
    },
  ];

  function handleSubmit(event: SubmitEvent) {
    if (!newTodoText) return;

    todos = [
      ...todos,
      { id: todos.length, text: newTodoText, completed: false },
    ];
    newTodoText = "";
  }
</script>

<main class="flex justify-center flex-col items-center mt-20 p-10">
  <h1 class="text-2xl">Todos</h1>
  <ul class="mt-2">
    {#each todos as todo}
      <li class="flex">
        <input type="checkbox" bind:checked={todo.completed} class="mr-1" />
        <p class={`text-lg ${todo.completed ? "line-through" : ""}`}>
          {todo.text}
        </p>
      </li>
    {/each}
  </ul>
  <form on:submit|preventDefault={handleSubmit}>
    <input
      type="text"
      bind:value={newTodoText}
      name="text"
      class="shadow-sm border-2 mt-3 p-1 rounded-md"
    />
    <button type="submit" class="shadow-sm rounded-md border-2 mt-3 p-1">
      Add
    </button>
  </form>
</main>
