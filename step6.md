# ステップ6

ローカルストレージによるデータの永続化

- 初期化: onMountフックを使ってアプリ起動時にlocalStorageからデータを読み込みます
- 自動保存: $effect(リアクティブな副作)を使ってtodosが変更されるたびに、localStorageへ自動保存します。

これにより、ページをリロードしてもTodoリストの内容が保持されるようになりました。

## src/routes/+page.svelte

```
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

<main>
  <h1>Todo App</h1>
  <input
    type="text"
    新しいタスク...
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
```
