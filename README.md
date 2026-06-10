# ThoughtStream Inbox

思考をCraftに即投稿するPWA。スマホ・PCどこからでも使える「脳のInbox」。

## コンセプト

Fast Notion / Obsidian Thino にインスパイアされた、気軽にメモを放り込める器。メモは日時自動付与でCraftのInboxドキュメントに集約される。

## 機能

- メモ入力 → Craftに即時保存
- 日時自動付与（`**[2026-06-10 14:32]**` 形式）
- タグ対応（スペースまたはカンマ区切り）
- PWA対応（スマホのホーム画面に追加可能）
- Service Workerによるオフライン対応
- 下書き自動保存（localStorageに保持）

## セットアップ

### 1. Craft APIの準備

1. Craftデスクトップアプリ → Settings → Imagine タブ
2. API connectionを作成（Inboxドキュメントを選択）
3. APIキーを作成してコピー

### 2. InboxドキュメントのドキュメントID取得

```
GET https://connect.craft.do/links/{connectionId}/api/v1/documents
Authorization: Bearer {apiKey}
```

レスポンスの `items[0].id` がドキュメントID。

### 3. PWAの設定

アプリを開いて右上の歯車アイコン → 以下を入力して保存：

- **Craft API URL**: `https://connect.craft.do/links/{connectionId}/api/v1`
- **APIキー**: CraftのImagineタブで発行したキー
- **InboxドキュメントID**: 上記で取得したID

## ホスティング

GitHub Pages: `https://takao1012.github.io/thoughtstream-pwa/`

## Craft API 仕様メモ

| 項目 | 内容 |
|---|---|
| ベースURL | `https://connect.craft.do/links/{connectionId}/api/v1` |
| 認証 | `Authorization: Bearer {apiKey}` |
| ブロック追加 | `POST /blocks` |
| リクエストボディ | `{ markdown: string, position: { pageId: string, position: "end" } }` |
| ドキュメント一覧 | `GET /documents` |

## 運用

溜まったメモはClaude.aiに読ませて整理・仕分け・ネタ提案に活用。Craft MCPが繋がっていればInboxドキュメントを直接読ませることも可能。
