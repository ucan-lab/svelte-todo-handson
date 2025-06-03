# ステップ2: 動的なデータ構造へのリファクタリング

動的なデータ構造へのリファクタリングをします。

- Todoリストのデータを配列（todos）として管理し、各Todoの状態（完了/未完了）も含めて型定義（TypeScriptの型）します。
- Svelteの{#each}構文を使って、配列から動的にリストを生成するようにリファクタリングします。
- 完了済みのTodoにはdoneクラスを動的に付与し、取り消し線が表示されるようにします。
- これにより、今後の機能追加（追加・削除・完了状態の切り替えなど）がしやすい構造になります。

## src/routes/+page.svelte

```svelte
<script lang="ts">
  // 修正
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
    <!-- 修正 -->
    {#each todos as todo, i}
      <li>
        <input type="checkbox" />
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

## [STEP3へ](step3.md)
