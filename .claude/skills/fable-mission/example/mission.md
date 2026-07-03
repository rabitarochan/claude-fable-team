# ミッション: TODO 管理 REST API

- slug: `example-todo-api`
- 開始日: 2026-06-29
- 状態: 進行中
- 発注者の依頼(原文のまま):
  > TODO 管理の REST API を作って。ユーザーごとに TODO を分けたい。認証は簡単でいいけど、ちゃんとテストは書いて

## ゴール

Express + SQLite で、ユーザーごとに分離された TODO 管理 REST API を作る。
認証は API キー方式(発注者が「簡単でいい」と明言)。

## 完了の定義(Definition of Done)

- [x] `npm test` が全件通る(CI 相当のクリーン環境で)
- [ ] API キー認証により、他ユーザーの TODO に一切アクセスできないことを curl で観測できる
- [ ] README に起動手順と API 一覧が載っており、その手順どおりで実際に起動できる

## 検証ハーネス(このプロジェクトのフィードバックループ)

| 装置 | コマンド | 所要時間の目安 |
|---|---|---|
| テスト(全体) | `npm test` | 約 15 秒 |
| テスト(部分) | `npm test -- <パターン>` | 数秒 |
| lint / 型検査 | `npm run lint && npm run typecheck` | 約 10 秒 |
| 起動・動作確認 | `npm start` → `curl localhost:3000/todos` | 起動約 2 秒 |

## 制約

- 依存は最小限(発注者の意向。フレームワークの追加導入は要相談)
- Node.js 22 / TypeScript

## スコープ外

- フロントエンド
- OAuth 等の本格認証(「後でやるかも」— 発注者談)
- デプロイ・ホスティング
