# 現在地(state): 英語化と GitHub 公開

> **このファイルが唯一の真実。** セッションはいつ死んでもよい。

- slug: `i18n-publish`
- フェーズ: Phase 4 — 進行中(4.1 総合検証 完了、公開ゲート待ち)
- 進捗: 完了 15 / 全 13+1+4 タスク(Phase 1〜3 全完了、Phase 4.1 完了)
- 最終更新: 2026-07-03 22:00
- 更新者: 指揮者(resume セッション)

## 次の一手(最重要)

**発注者の公開最終承認を待っている。**

承認されたら、以下のフロー(計画 4.2〜4.4)を実行:

(a) `README.md` の marketplace add 行を `/plugin marketplace add rabitarochan/claude-fable-team` に確定してコミット  
(b) `gh repo create rabitarochan/claude-fable-team --public --source=. --push` で GitHub に公開リポジトリ作成・push  
(c) `git tag v0.1.0 && git push origin v0.1.0` で v0.1.0 リリースタグ付与・push  
(d) 4.4 導入テスト — 実プロジェクトで `/plugin marketplace add rabitarochan/claude-fable-team` → `/plugin install fable-team@fable-team` → `/fable-team:init` を発注者協力で完走し、日本語で対話されることを確認

## 進行中・中断点

なし(Phase 3 成果はコミット済み、ゲート待ち)。

## 検証状態

- 検証済み:
  - フレームワーク内部の英語化 — 日本語残存 grep 0(agents/skills/.claude-plugin)、`claude plugin validate .` 通過、逆翻訳レビュー 3 体の must-fix/recommended 全対応、状態トークン横断統一
  - gh 認証(rabitarochan、repo スコープ有)、翻訳対象規模 agents 7 / skills 28 の baseline 確認
  - 4.1 総合検証 — 日本語残存 0 / validate / 英日相互リンク / LICENSE=MIT rabitarochan / 言語規則 / 英語版本文クリーン の全 6 項目 green「公開可」
- 未検証: 公開後の導入一連(Phase 4.4 導入テスト)

## ブロッカー・注意

- ※ セッションによりロール実行手段が変わる。resume 時に再確認すること。本セッションでは fable-team:* 専用エージェント(verifier 等)が利用可能
- 発注者は英語レビューをしない。承認・検収はすべて日本語で成立させること(逆翻訳レビュー必須)
