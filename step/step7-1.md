# ステップ7-1: tailwindcssのインストール

## tailwindcssとは

https://tailwindcss.com

小さな役割のクラス（ユーティリティクラス）を最優先して使うスタイルのCSSフレームワークです。

「Tailwind CSS IntelliSense」の拡張機能を入れると補完が効くのでおすすめ
https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss

## tailwindcssインストール

公式サイトを参考にインストールします。

https://tailwindcss.com/docs/installation/framework-guides/sveltekit

```bash
$ npm install -D tailwindcss @tailwindcss/vite
```

- `-D` `--save-dev` の省略オプション
  - package.jsonの "devDependencies" に入る
  - `--save-dev` は開発時にのみ必要なライブラリを入れたい時に使う
  - 本番環境では要らないもの
- tailwindcss v4 2025年1月リリース
  - postcss, autoprefixerが同梱
    - postcss はCSSツールを作るためのフレームワーク
    - autoprefixer ブラウザの互換性を確保する(古いブラウザでも正しく動作させる)

### vite.config.ts を編集する

[Vite](https://ja.vite.dev) の設定ファイルを編集します。

```ts
import { sveltekit } from '@sveltejs/kit/vite';
import { defineConfig } from 'vite';
import tailwindcss from '@tailwindcss/vite'; // 追加

export default defineConfig({
  plugins: [
    tailwindcss(), // 追加
    sveltekit(),
  ]
});
```

### src/app.css を作成する

グローバルなCSSファイルです。

```css
@import "tailwindcss";
```

### src/routes/+layout.svelte を作成する

全ページ共通の CSS を適用し、ページ内容をそのまま表示する最小限のレイアウトファイルを作成します。

```svelte
<script>
  let { children } = $props();
  import "../app.css";
</script>
{@render children()}
```

- `let { children } = $props();`
  - $props() は Svelte5 の新しい構文で、「このコンポーネントに渡された props を取得する関数」
    - https://svelte.jp/docs/svelte/$props
  - このコンポーネントに渡された props（プロパティ） から children を取り出す
  - children はこのレイアウトの中に含まれるページコンテンツを指す
- `import "../app.css";`
  - グローバル CSS を読み込む
  - `+layout.svelte` で読み込むことで、すべてのページに適用される
- `{@render children()}`
  - children() をレンダリング(描画)します
    - 子ページ(+page.svelteなど) の 内容(children) を描画する
  - https://svelte.jp/docs/svelte/@render

一旦おまじないとして覚えておく。

開発用サーバーを再起動します。
`control` + `c` で止める。

```bash
$ npm run dev
```

tailwindcssが導入できたか確認するためにファイルを作ります。

### src/routes/test/+page.svelte を作成する

```svelte
<h1 class="text-3xl font-bold underline">Hello world!</h1>

<style lang="postcss">
  @reference "tailwindcss";
  :global(html) {
    background-color: theme(--color-gray-100);
  }
</style>
```

http://localhost:5173/test

## [STEP7-2へ](step7-2.md)
