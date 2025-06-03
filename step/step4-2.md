# ステップ4-2: ルーン($state)の導入

変数の初期化を $state に置き換えることで配列を push や splice したときに再代入せずとも状態が更新されたときに関数を再実行します。

- ルーン($state)の導入
  - https://svelte.jp/blog/runes
- ルーン文字には `$` 接頭辞がある
- インポートする必要なく、言語の一部として扱える

## src/routes/+page.svelte

```svelte
<script lang="ts">
  type Todo = {
    text: string;
    done: boolean;
  };

  // 修正
  let todos: Todo[] = $state([
    { text: 'ミーティング資料を作る', done: false },
    { text: 'プルリクエストをレビューする', done: true },
    { text: '本番リリースをする', done: false }
  ]);

  // 修正
  let newTodo: string = $state('');

  function addTodo() {
    if (newTodo.trim()) {
      // 修正
      todos.push({ text: newTodo, done: false });
    }
  }
</script>

<main>
  <h1>Todo App</h1>

  <input type="text" placeholder="新しいタスク..." bind:value={newTodo} />

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

## [STEP4-3へ](step4-3.md)
