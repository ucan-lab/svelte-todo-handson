<script lang="ts">
  import { onMount } from 'svelte';

  type Todo = {
    text: string;
    done: boolean;
  };

  let todos = $state([] as Todo[]);
  let newTodo: string = $state('');
  let isInitialized: boolean = $state(false);

  onMount(() => {
    if (typeof window !== 'undefined') {
      try {
        const savedTodos = localStorage.getItem('todos');
        if (savedTodos) {
          todos = JSON.parse(savedTodos);
        }
      } catch (e) {
        console.error('Failed to load todos from localStorage:', e);
      } finally {
        isInitialized = true;
      }
    }
  });

  $effect(() => {
    if (isInitialized && typeof window !== 'undefined') {
      try {
        localStorage.setItem('todos', JSON.stringify(todos));
      } catch (e) {
        console.error('Failed to save todos to localStorage:', e);
      }
    }
  });

  function addTodo() {
    if (newTodo.trim()) {
      todos.push({ text: newTodo, done: false });
      newTodo = '';
    }
  };

  function deleteTodo(index: number) {
    todos.splice(index, 1);
  };
</script>

<main class="min-h-screen bg-gray-100 flex flex-col items-center py-10">
  <h1 class="text-4xl font-bold text-gray-800 mb-8">Todo App</h1>

  <div class="flex items-center gap-4 mb-6">
    <input
      type="text"
      placeholder="新しいタスク..."
      bind:value={newTodo}
      onkeydown={(e) => {
        if (e.key === 'Enter' && !e.isComposing) {
          addTodo();
        }
      }}
      class="w-64 p-2 border bg-white border-gray-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500"
    />
    <button
      onclick={addTodo}
      disabled={!newTodo.trim()}
      class="px-4 py-2 bg-blue-500 text-white font-semibold rounded-lg shadow-md hover:bg-blue-600 disabled:bg-gray-300 disabled:cursor-not-allowed"
    >
      追加
    </button>
  </div>

  <ul class="w-full max-w-md">
    {#each todos as todo, i}
      <li class="flex items-center justify-between bg-white p-4 rounded-lg shadow-sm mb-2">
        <div class="flex items-center gap-3">
          <input
            type="checkbox"
            bind:checked={todo.done}
            class="h-5 w-5 text-blue-500 focus:ring-blue-500 border-gray-300 rounded"
          />
          <span class={`text-lg ${todo.done ? 'line-through text-gray-400' : 'text-gray-700'}`}>
            {todo.text}
          </span>
        </div>
        <button
          onclick={() => deleteTodo(i)}
          class="text-red-500 font-semibold hover:underline"
        >
          削除
        </button>
      </li>
    {/each}
  </ul>
</main>

<style>
</style>
