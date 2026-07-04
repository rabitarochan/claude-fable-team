# Mission: ブレインストーミング支援資産の新設

- slug: `brainstorm-asset`
- Start date: 2026-07-04
- Status: in progress
- The user's request (verbatim):
  > Fable の力を借りたくて、Fable で mission を始めます。
  > あなたが引き継いだ中に、ブレインストーミング (プロジェクトを始める前のアイディア出し) に関するものはありますか？
  > もしなければ、同じく引き継ぎ資料として agent や skills を作成してください。
  >
  > 資料作成などの指示は、Fable Team を活用してください。これはあなたの資料が使えるかどうかのドッグフーディングです。

## Goal

Fable 5 の引き継ぎ資産にブレインストーミング(プロジェクト開始前のアイディア出し)支援が存在しないことを確認済み
(リポジトリ全域 grep でヒット 0、HANDOFF.md には近縁の「Judge Panel」パターンのみ)。
そこで、引き継ぎ資料と同品質のコマンドスキル `/fable-team:brainstorm` を新設し、
Fable Team 自身の運用(委任・検証・記録)で作り上げる(ドッグフーディング)。

## Definition of Done

- [ ] `skills/brainstorm/SKILL.md` が存在し、規約に準拠している: frontmatter description に "Use when…" と "/fable-team:brainstorm" トリガ句 / 本文に (a) 手順(問題枠づけ→発散→収束→goal/DoD 草案化→intake ルート判定) (b) fenced の出力サマリブロック (c) 小さなレンズカタログ (d) 「対ユーザー対話はユーザー言語で」規則 / 内部は全英語(日本語文字 grep = 0)
- [ ] `claude plugin validate .` が exit 0
- [ ] reviewer(Opus)の逆評価で未対応指摘 0(修正サイクル最大2周)
- [ ] ドッグフーディング: 実在のあいまいな題材で新スキルによるブレストを1回実施し、出力(goal 草案+観測可能な DoD 草案)が `/fable-team:mission` または `/fable-team:task` の intake に手戻りなく受理された証拠が journal にある。対話がユーザー言語(日本語)で行われた
- [ ] README.md 構造ツリーに brainstorm 行が追加され、CHANGELOG.md に証拠シグナル付きエントリが存在する
- [ ] 変更セット(SKILL.md + README 差分 + CHANGELOG)がユーザーに提示され、承認されている

## Verification harness (this project's feedback loop)

| Check | Command | Approx. duration |
|---|---|---|
| Tests (full) | なし(自動テスト・CI は存在しない) | - |
| Tests (partial) | なし | - |
| Lint / type check | `claude plugin validate .`(プラグイン構造の検証) | 約 2 秒 |
| Launch & smoke check | `/plugin marketplace add <本リポジトリ>` → `/plugin install fable-team@fable-team` → 実プロジェクトで動作確認(最終確認はユーザー実施のインストールテスト) | 数分 |

スキルの「挙動」を測る自動テストは存在しないため、挙動検証は Phase 2 のドッグフーディング(Conductor-in-the-loop)で担保する。

## Constraints

- フレームワーク変更(`skills/` 配下)はユーザー承認が必須。CHANGELOG.md に証拠シグナル付きで記録する(growth-loop 規律)
- フレームワーク内部は英語、ユーザーとの対話はユーザー言語(新スキル自身もこの規則に従うこと)
- **Bloat is death**: 追加は `skills/brainstorm/SKILL.md` 1ファイルのみ。列挙点の差分は README 構造ツリー + CHANGELOG のみ。新エージェント・playbook.md・templates/・example/・新状態ディレクトリ・マニフェスト変更はすべて作らない
- rules.md は変更しないため、導入済みプロジェクトへの再 init 伝播は不要

## Out of scope

- 専用 ideator エージェントの新設(反復ロール化して初めて再考 — plan.md「再考の条件」参照)
- playbook.md への分割と Playbooks 表への追加(単一ファイルに収まらなくなったら再考)
- ブレスト記録の永続化(`.fable-team/brainstorms/` 等)— セッションを跨ぐならそれは mission に昇格すべきもの
- フル・デザイン思考手法カタログ(SCAMPER / Six Hats / Crazy 8s …)— レンズは小さな核のみ。残りは grow バックログ行き
