# ステップ7-1

## tailwindcssとは

https://tailwindcss.com

小さな役割のクラス（ユーティリティクラス）を最優先して使うスタイルのCSSフレームワークです。

「Tailwind CSS IntelliSense」の拡張機能を入れると補完が効くのでおすすめ
https://marketplace.visualstudio.com/items?itemName=bradlc.vscode-tailwindcss

## tailwindcssインストール

公式サイトを参考にインストールします。

https://tailwindcss.com/docs/installation/framework-guides/sveltekit

```
$ npm install -D tailwindcss @tailwindcss/vite
```

- `-D` `--save-dev` の省略オプション
  - package.jsonの "devDependencies" に入る
  - `--save-dev` は開発時にのみ必要なライブラリを入れたい時に使う
  - 本番環境では要らないもの
- tailwindcss v4 2025年1月リリース
  - postcss, autoprefixerが同梱

vite.config.ts を編集する

```
import { sveltekit } from '@sveltejs/kit/vite';
import { defineConfig } from 'vite';
import tailwindcss from '@tailwindcss/vite'; // 追加
export default defineConfig({
  plugins: [
    sveltekit(),
    tailwindcss(), // 追加
  ],
});
```

src/app.css を新しく作る
グローバルなCSSファイルです。

```
@import "tailwindcss";
```

src/routes/+layout.svelte を新しく作る
全ページ共通のレイアウトや処理を定義するファイルです。

```
<script>
  let { children } = $props();
  import "../app.css";
</script>
{@render children()}
```

- 一旦おまじないとして
  - https://svelte.jp/docs/svelte/$props
  - https://svelte.jp/docs/svelte/@render

開発用サーバーを再起動します。
`control` + `c` で止める。

```
$ npm run dev
```

tailwindcssが導入できたか確認するためにファイルを作ります。

src/routes/test/+page.svelte

```
<h1 class="text-3xl font-bold underline">
  Hello world!
</h1>
<style lang="postcss">
  @reference "tailwindcss";
  :global(html) {
    background-color: theme(--color-gray-100);
  }
</style>
```

http://localhost:5173/test
