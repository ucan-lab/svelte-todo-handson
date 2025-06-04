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
</script>

<main>
  <h1>Todoアプリ</h1>

  <input type="text" placeholder="新しいタスク..." />

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
