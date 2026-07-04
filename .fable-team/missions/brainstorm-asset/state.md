# Current state: ブレインストーミング支援資産の新設

> **This file is the single source of truth.** Any session may die at any moment.
> Update it after every task completion and every checkpoint.
> If this file and reality (code, test results) disagree, reality is the truth. Record it in the journal and fix this file.

- slug: `brainstorm-asset`
- Phase: Phase 1 — 資産のオーサリング(完了・ゲート通過)
- Progress: 6 of 13 tasks done
- Last updated: 2026-07-04 09:35
- Updated by: scribe

## Next move (most important)

**Phase 1 ゲート PASS(validate exit 0 / 未対応指摘 0)。ユーザーの中間報告確認後、Phase 2 → 2.1 から再開。**

Phase 2 の 2.1(実ブレスト・ドッグフーディング)では、新スキル `skills/brainstorm/SKILL.md` の手順に従い、**ユーザーと日本語で実ブレストを1回実施**する。題材候補:
- growth inbox(`.fable-team/growth/inbox.md`)の未処理シグナル
- HANDOFF.md の未カバー領域
- ユーザー持ち込みのあいまいなアイデア

出力サマリ(問題枠づけ / 探索した選択肢 / 収束方向 / **goal 草案 + 観測可能な DoD 草案** / 推奨 intake ルート)を含むブレスト・サマリを生成し、要約を journal に記録。
その後、2.2 で verifier に intake 適合検証を委任(出力サマリが `/fable-team:mission`(または task)intake に手戻りなく受理できるか確認)。

**再開コマンド**: `/fable-team:resume` または `/fable-team:work`

## In progress / stopping point

**Phase 1 ゲート通過により停止。Phase 2 の実ブレスト(2.1)はユーザーとの対話が必須のため、ユーザー確認待ち。**

## Verification status

- **Verified**:
  - 1.1: SKILL.md 存在・74行・frontmatter 完備・日本語grep 0・validate exit 0・単一ファイル制約遵守
  - 1.2: README.md 構造ツリー更新(brainstorm 行追加 + 計数行整合)、git diff で README.md のみ確認
  - 1.3: validate exit 0(Conductor 実行確認)
  - 1.2b: README.ja.md 同期(brainstorm 行追加・位置同じ・計数行整合)、git diff で README.ja.md のみ確認
  - 1.4: reviewer 逆評価(全7観点 PASS / APPROVE-WITH-FIXES)、3件指摘を記録
  - 1.5: 修正3件反映(日本語 grep=0 / validate exit 0 / 最終76行)、Conductor 全文スポットチェック受理
- **Unverified**:
  - Phase 2 ドッグフーディング一式(2.1-2.4): ユーザーとの実対話待ち
  - Phase 3(3.1-3.3): Phase 2 完了後
- 偵察完了済み: ブレスト資産不存在 / スキル規約 / 列挙点 / 検証ハーネス の4観点

## Blockers / notes

- **ユーザーの中間報告確認待ち**: Phase 2 の実ブレストはユーザーとの対話が必須のため、再開前にユーザーの承認・題材指定が必要
- 注意: フレームワーク変更はユーザー承認 + CHANGELOG 記録が必須(HQ リポジトリ規則)。Phase 3 の 3.2 が最終承認点
- 注意: rules.md は変更しない計画のため、導入済みプロジェクトへの再 init 伝播は不要(変更したら必要になるので注意)
