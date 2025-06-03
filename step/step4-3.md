# ステップ4-3: 新しいタスクの追加機能の強化

Todoの追加時の機能を強化

- 入力欄のクリアとEnterキー対応
- タスク追加後にnewTodo = ''で入力欄をクリアします。
- 入力欄でEnterキーを押すとタスクが追加されるように、onkeydownイベントを追加しています。

## src/routes/+page.svelte

```svelte
<script lang="ts">
  type Todo = {
    text: string;
    done: boolean;
  };

  let todos: Todo[] = $state([
    { text: 'ミーティング資料を作る', done: false },
    { text: 'プルリクエストをレビューする', done: true },
    { text: '本番リリースをする', done: false }
  ]);

  let newTodo: string = $state('');

  function addTodo() {
    if (newTodo.trim()) {
      todos.push({ text: newTodo, done: false });
      newTodo = ''; // 修正
    }
  }
</script>

<main>
  <h1>Todo App</h1>

  <!-- 修正 -->
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
        <button>削除</button>
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

## [STEP5へ](step5.md)
