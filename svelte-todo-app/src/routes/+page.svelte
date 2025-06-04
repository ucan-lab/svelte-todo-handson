<script lang="ts">
  import { onMount } from 'svelte';

  type Todo = {
    text: string;
    done: boolean;
  };

  let newTodo: string = $state('');

  let todos = $state([] as Todo[]);
  let isInitialized: boolean = $state(false);

  function addTodo() {
    if (newTodo.trim()) {
      todos.push({ text: newTodo, done: false });
      newTodo = '';
    }
  }

  function deleteTodo(index: number) {
    todos.splice(index, 1);
  }

  onMount(() => {
    // ブラウザ上で動いてる時のみ。SSR中(Node.js実行環境)は undefined
    if (typeof window !== 'undefined') {
      try {
        // ローカルストレージから TODO JSON文字列を取得
        const savedTodos = localStorage.getItem('todos');
        if (savedTodos) {
          todos = JSON.parse(savedTodos); // JSON文字列を TODO オブジェクトに変換
        }
      } catch (e) {
        console.error('Failed to load todos from localStorage:', e);
      } finally {
        isInitialized = true; // 初期化完了
      }
    }
  });

  $effect(() => {
    if (isInitialized && typeof window !== 'undefined') {
      try {
        // ローカルストレージへTODOオブジェクトをJSON文字列で保存
        localStorage.setItem('todos', JSON.stringify(todos));
      } catch (e) {
        console.error('Failed to save todos to localStorage:', e);
      }
    }
  });
</script>

<main>
  <h1>Todo App</h1>

  <input
    type="text"
    placeholder="新しいタスク..."
    bind:value={newTodo}
    onkeydown={(e) => {
      if (e.key === 'Enter' && !e.isComposing) {
        addTodo();
      }
    }}
  />

  <button onclick={addTodo} disabled={!newTodo.trim()}>追加</button>

  <ul>
    {#each todos as todo, i}
      <li>
        <input type="checkbox" bind:checked={todo.done} />
        <span class={todo.done ? 'done' : ''}>{todo.text}</span>
        <button onclick={() => deleteTodo(i)}>削除</button>
      </li>
    {/each}
  </ul>
</main>

<style>
  span.done {
    text-decoration: line-through;
  }

  button[disabled] {
    opacity: 0.5;
    cursor: not-allowed;
  }
</style>
