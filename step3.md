# ステップ3

Todoの完了状態をチェックボックスで切り替えられるようにする。

- チェックボックス（<input type="checkbox">）にbind:checked={todo.done}を追加し、各Todoの完了状態（done）とチェックボックスの状態を双方向バインディングしました。
- これにより、チェックボックスをクリックすると、該当のTodoの完了状態（done）が自動的に切り替わるようになりました。
- 完了状態が切り替わると、doneクラスが付与され、取り消し線の表示も動的に反映されます。

## src/routes/+page.svelte

```
<script lang="ts">
  type Todo = {
    text: string;
    done: boolean;
  };

  let todos: Todo[] = [
    { text: 'ミーティング資料を作る', done: false },
    { text: 'プルリクエストをレビューする', done: true },
    { text: '本番リリースをする', done: false },
  ];
</script>

<main>
  <h1>Todoアプリ</h1>

  <input
    type="text"
    新しいタスク...
  />
  <button>追加</button>

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
</style>
```
