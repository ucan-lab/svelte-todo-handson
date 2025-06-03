## SvelteKitError: Not found: /.well-known/appspecific/com.chrome.devtools.json

```
$ npm run dev
```

Chromeで開発者ツールを開いたときに次のエラーが出た場合
SvelteKitError: Not found: /.well-known/appspecific/com.chrome.devtools.json

```
$ google-chrome-canary --enable-features=DevToolsWellKnown、DevToolsAutomaticFileSystems
```

Chromium (M-135 以降で利用可能)で自動ワークスペース フォルダーという機能が追加されました。

https://chromium.googlesource.com/devtools/devtools-frontend/+/main/docs/ecosystem/automatic_workspace_folders.md

エラーメッセージが気になる人はフラグを無効化するか、ワークスペースフォルダーを作成してください。

- chrome://flags#devtools-project-settings
- chrome://flags#devtools-automatic-workspace-folders
