---
name: init
description: >
  Fable Team をプロジェクトに導入する。プラグインのインストール後、対象プロジェクトで
  「/fable-team:init」「Fable Team をセットアップして」「Fable Team を導入して」と
  言われたときに使う。.fable-team/(状態ディレクトリ)を作成し、プロジェクトの
  CLAUDE.md にチーム規約を組み込む。再実行すると規約セクションだけを最新版に更新する(冪等)。
---

# /fable-team:init — プロジェクトへの導入

Fable Team の頭脳(エージェント・スキル)はプラグインが持ってくる。
このスキルは残りの 2 つ —— **状態の置き場**と**常時ロードされる規約** —— を対象プロジェクトに用意する。

## 手順

1. **規約の正本を読む**: `${CLAUDE_PLUGIN_ROOT}/skills/init/rules.md`

2. **状態ディレクトリを作成する**(既存のものには触らない):
   - `.fable-team/growth/inbox.md` ← `${CLAUDE_PLUGIN_ROOT}/skills/init/templates/inbox.md` をコピー
   - `.fable-team/growth/changelog.md` ← 同 `templates/changelog.md` をコピー
   - `.fable-team/missions/` は最初のミッションが作るので、今は作らない

3. **プロジェクトの CLAUDE.md に規約を組み込む**(既存ファイルの変更なので、実行前にユーザーへ一言確認する):
   - `<!-- fable-team:rules:start -->` 〜 `<!-- fable-team:rules:end -->` のマーカーで囲んで、
     rules.md の内容を挿入する
   - **既にマーカーがある場合は、マーカー間だけを最新版で置き換える**(再実行 = 規約の更新。
     マーカー外のプロジェクト固有規約には一切触れない)
   - CLAUDE.md が存在しなければ新規作成する

4. **完了報告**(3 行で):
   - 単発タスク(1 セッション完結)は `/fable-team:task`
   - 長期タスク(セッションをまたぐ)は `/fable-team:mission`
   - 迷ったら「明日も続きをやるか?」で判断

## 注意

- マーカー内は init が管理する領域である。プロジェクト固有の規則(成長ループで収穫した
  規則を含む)は**マーカーの外**に書く
- git リポジトリなら、導入をコミットすることを提案する
