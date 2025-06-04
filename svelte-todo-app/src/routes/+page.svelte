<main>
  <h1>Todoアプリ</h1>

  <input type="text" placeholder="新しいタスク..." />

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
