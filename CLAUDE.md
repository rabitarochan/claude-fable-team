# Fable Team — HQ リポジトリ規約

このリポジトリは Fable Team(Claude Plugin)の開発リポジトリ兼司令部である。
チーム規約の正本は init スキルに同梱されており、以下に取り込む:

@skills/init/rules.md

## このリポジトリ固有の規約

- ここは**フレームワーク自体の開発場所**である。フレームワーク(`agents/` / `skills/` /
  規約の正本 `skills/init/rules.md`)への変更はユーザー承認制で、根拠シグナルつきで
  `CHANGELOG.md` に記録する(成長ループの規律)
- プラグインとして配布されるのは `.claude-plugin/` + `agents/` + `skills/`。
  状態(`.fable-team/`)とドキュメント(README / HANDOFF / CHANGELOG)は配布物ではない
- 規約の正本を変更したら、導入済みプロジェクトには `/fable-team:init` の再実行で
  反映される(マーカー間の置き換え)
- 動作確認の手順: `claude plugin validate .` →
  `/plugin marketplace add <このリポジトリのパス>` → `/plugin install fable-team@fable-team` →
  実プロジェクトで `/fable-team:init`
