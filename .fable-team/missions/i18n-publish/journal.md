# 作業日誌: 英語化と GitHub 公開

> **追記専用。** 過去のエントリを書き換え・削除しない。

---

## 2026-07-03 17:45 — 指揮者(Fable 5、立ち上げセッション)

- **やったこと**: ミッション立ち上げ。偵察(gh 認証確認 → rabitarochan / repo スコープ有で
  公開可能。日本語残存ベースライン → agents 7 + skills 28 ファイル)。3 層言語設計で計画立案
- **分かったこと**: 公開の技術的ブロッカーなし。翻訳対象は約 40 ファイル
- **判断と理由**: ①glossary を全翻訳に先行させる(並列翻訳の用語割れ防止)
  ②品質保証は逆翻訳レビュー方式(発注者が英語を読まずに検収できる唯一の方法)
  ③HANDOFF のみ日本語を原本とする(Fable 5 の思想の原典であるため)
- **次へ**: 発注者の計画承認待ち

## 2026-07-03 17:49 — 指揮者(Fable 5)

- **やったこと**: 計画承認を受け Phase 1 実行。タスク 1.1 — glossary.md 作成
  (中核概念・成長ループ用語・アフォリズム 15 句の定訳・文体規則)。
  タスク 1.2 — rules.md に挿入する言語規則の英文を設計:

  > ## Language
  > The framework's internals are English; the user's experience is not.
  > - Always interact with the user in the user's language.
  > - Mission state files (mission.md / plan.md / state.md / journal.md), growth-signal
  >   entries, reports, and anything else the user reads day-to-day are written in the
  >   user's language as well.
  > - When a project has an established working language, follow it.

- **分かったこと**: —
- **判断と理由**: アフォリズムは「一字一句この訳で統一」とした(並列翻訳者の意訳が
  一番怖いのはここ。定訳固定が逆翻訳レビューの判定基準にもなる)
- **次へ**: Phase 1 ゲート(発注者の日本語承認)→ 承認後 Phase 2 並列翻訳へ
