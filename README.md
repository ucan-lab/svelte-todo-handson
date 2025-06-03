# Svelteって何？軽量＆高速なWeb開発ToDoアプリハンズオン

https://phper-oop.connpass.com/event/354894

## 今回のゴール

https://svelte-todo-handson.vercel.app

![](screenshot/vercel-7.png)

## 準備

```
$ mise use node@22.16.0
```

- [miseについて](https://qiita.com/ucan-lab/items/f7f010ee2d13ab99203c)

```
$ node -v
v22.16.0

$ npm -v
10.9.2
```

### エディタにSvelte拡張機能をインストール

Visual Studio Code or Cursorの人は [Svelte for VS Code](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode) の拡張機能をインストールすると補完が効くようになる

## Svelteプロジェクトの作成

```
$ npx sv create svelte-todo-app
```

- npm はnode package manager = パッケージの管理ツール
- npx はnode package executer = パッケージの実行を行うツール
- sv はSvelteアプリケーションの作成と管理のためのツールキット
  - https://svelte.jp/docs/cli/overview

設問には次のように回答してください

```
$ npx sv create svelte-todo-app
┌  Welcome to the Svelte CLI! (v0.8.7)
│
◇  Which template would you like?
│  SvelteKit minimal # テンプレート選択: 最小構成でインストールする
│
◇  Add type checking with TypeScript?
│  Yes, using TypeScript syntax # TypeScriptを使う
│
◆  Project created
│
◇  What would you like to add to your project? (use arrow keys / space bar)
│  prettier, eslint # コードフォーマッター、構文のコードチェックリンター
│
◆  Successfully setup add-ons
│
◇  Which package manager do you want to install dependencies with?
│  npm # パッケージ管理ツール
│
◆  Successfully installed dependencies
│
◇  Successfully formatted modified files
│
◇  Project next steps ─────────────────────────────────────────────────────╮
│                                                                          │
│  1: cd svelte-todo-app                                                   │
│  2: git init && git add -A && git commit -m "Initial commit" (optional)  │
│  3: npm run dev -- --open                                                │
│                                                                          │
│  To close the dev server, hit Ctrl-C                                     │
│                                                                          │
│  Stuck? Visit us at https://svelte.dev/chat                              │
│                                                                          │
├──────────────────────────────────────────────────────────────────────────╯
│
└  You're all set!
```

インストールしたら開発用サーバーを起動する

```
$ cd svelte-todo-app

# Git管理したい方
$ git init # このリポジトリをクローンしてそのまま使うなら不要
$ git add -A
$ git commit -m "Initial commit"

# 開発用のサーバーを起動する
$ npm run dev -- --open
```

- `npm run dev`
  - package.json の "scripts" に定義された dev コマンドを実行
    - 通常は vite dev
- `--` npm にとってのオプションの区切り
  - これ以降の引数を npm ではなくスクリプト側に渡す
- `--open` Viteのオプション: ブラウザを開く

http://localhost:5173

![](screenshot/svelte-1.png)

## 宗教上の理由でインデントをスペースに変更する

`.prettierrc`

```diff
{
-	"useTabs": true,
+	"useTabs": false,
	"singleQuote": true,
	"trailingComma": "none",
	"printWidth": 100,
	"plugins": ["prettier-plugin-svelte"],
	"overrides": [
		{
			"files": "*.svelte",
			"options": {
				"parser": "svelte"
			}
		}
	]
}
```

次のコマンドで適用されます。

```
$ npm run format
```

VSCode or Cursor の場合、設定(Command+,)から `Editor:Format On Save` を有効にすると、保存時に自動でフォーマットされます。

## ディレクトリ構成

```
svelte-todo-app/
├── src/
│   ├── lib/
│   │   └── ...         # コンポーネントやユーティリティの再利用ライブラリ
│   ├── routes/
│   │   ├── +page.svelte  # "/" ルートのページ（Svelte コンポーネント）
│   │   └── +page.ts      # （任意）ページ用のロード関数（load()）
│   ├── app.css         # アプリ全体（グローバル）に影響するCSS
│   ├── app.html        # HTMLテンプレート
│   └── ...             # 他にも hooks.server.ts や error.svelte などが入ることも
├── static/             # 公開静的ファイル（画像やfaviconなど）
│   └── favicon.png
├── svelte.config.js    # SvelteKit の設定ファイル
├── vite.config.ts      # Vite のビルド設定
├── tsconfig.json       # TypeScript 設定
├── package.json
└── README.md
```

### src/

アプリケーションのメインソースコードが入るディレクトリ。

### src/routes/

URLルーティングに対応するファイル/ディレクトリ。

- +page.svelte → ページコンポーネント
- +page.ts → データフェッチのための load 関数を定義できる
- +layout.svelte / +layout.ts でレイアウト共通化も可能

```
routes/
├── +page.svelte       # /
├── about/
│   └── +page.svelte   # /about
└── blog/
    ├── +page.svelte   # /blog
    └── [slug]/
        └── +page.svelte  # /blog/hello-world
```

## ハンズオン

- [STEP1: 静的なTodoリストの作成](step/step1.md)
- [STEP2: 動的なデータ構造へのリファクタリング](step/step2.md)
- [STEP3: Todoの完了状態をチェックボックスで切り替え](step/step3.md)
- STEP4: Todoの追加機能の実装
  - [STEP4-1: 新しいタスクの追加](step4-step/1.md)
  - [STEP4-2: ルーン($state)の導入](step4-step/2.md)
  - [STEP4-3: 新しいタスクの追加機能の強化](step4-step/3.md)
- [STEP5: タスクの削除](step/step5.md)
- [STEP6: データの永続化](step/step6.md)
- STEP7: デザインの強化
  - [STEP7-1: tailwindcssのインストール](step7-step/1.md)
  - [STEP7-2: tailwindcssの実装](step7-step/2.md)
- [STEP8: デプロイ](step/step8.md)
