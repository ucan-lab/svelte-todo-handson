# ステップ4-1: 新しいタスクの追加

Todoの追加機能の実装

- 新しいタスクを入力し、「追加」ボタンでリストに追加できるようにします。
- 入力値はnewTodoで管理し、addTodo関数でtodos配列にpushします。
- Svelteが配列の変更を検知できるよう、todos = todosで再代入しています。

## src/routes/+page.svelte

```svelte
<script lang="ts">
  type Todo = {
    text: string;
    done: boolean;
  };

  let todos: Todo[] = [
    { text: 'ミーティング資料を作る', done: false },
    { text: 'プルリクエストをレビューする', done: true },
    { text: '本番リリースをする', done: false }
  ];

  // 修正
  let newTodo: string = '';

  function addTodo() {
    if (newTodo.trim()) {
      todos.push({ text: newTodo, done: false });
      todos = todos;
    }
  }
</script>

<main>
  <h1>Todo App</h1>

  <!-- 修正 -->
  <input type="text" placeholder="新しいタスク..." bind:value={newTodo} />

  <!-- 修正 -->
  <button onclick={addTodo} disabled={!newTodo.trim()}>追加</button>

  <ul>
    {#each todos as todo, i}
      <li>
        <input type="checkbox" bind:checked={todo.done} />
        <span class={todo.done ? 'done' : ''}>{todo.text}</span>
        <button>削除</button>
      </li>
    {/each}
  </ul>
</main>

<style>
  span.done {
    text-decoration: line-through;
  }

  /* 修正 */
  button[disabled] {
    opacity: 0.5;
    cursor: not-allowed;
  }
</style>
```

## [STEP4-2へ](step4-2.md)
