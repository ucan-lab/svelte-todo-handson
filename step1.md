# ステップ1でやること

静的なTodoリストの作成します。

- Svelteの基本的な構造を使って、静的なTodoリスト画面を作成します
- Todoの項目（liタグ）を3つ用意し、それぞれに「ミーティング資料を作る」「プルリクエストをレビューする」「本番リリースをする」といったサンプル文言を表示します
- 2つ目のTodo（「プルリクエストをレビューする」）には完了済みを表すため、spanタグにdoneクラスを付与し、取り消し線が表示されるようにします
- CSSで.doneクラスに取り消し線のスタイルを追加します

## src/routes/+page.svelte

```
<main>
  <h1>Todoアプリ</h1>

  <input
    type="text"
    placeholder="新しいタスク..."
  />
  <button>追加</button>

  <ul>
    <li>
      <input type="checkbox" />
      <span>ミーティング資料を作る</span>
      <button>削除</button>
    </li>
    <li>
      <input type="checkbox" />
      <span class="done">プルリクエストをレビューする</span>
      <button>削除</button>
    </li>
    <li>
      <input type="checkbox" />
      <span>本番リリースをする</span>
      <button>削除</button>
    </li>
  </ul>
</main>

<style>
  span.done {
    text-decoration: line-through;
  }
</style>
```
