## src/routes/+page.svelte

```
<script lang="ts">
  type Todo = {
    text: string;
    done: boolean;
  };

  let todos: Todo[] = $state([
    { text: 'ミーティング資料を作る', done: false },
    { text: 'プルリクエストをレビューする', done: true },
    { text: '本番リリースをする', done: false },
  ]);

  let newTodo: string = $state('');

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
