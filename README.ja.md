# Fable Team

[English](README.md)

Fable 5 が引退した世界で、**Opus / Sonnet / Haiku の分業**により Fable 5 の
「長期タスクを最後まで完遂する能力」を再現する **Claude Code プラグイン**。

Fable 5 本人による引き継ぎ資料は [HANDOFF.ja.md](HANDOFF.ja.md) にある。

## インストール

```
# 1. マーケットプレイスを追加(ローカル試用ならこのリポジトリのパス)
/plugin marketplace add rabitarochan/claude-fable-team

# 2. プラグインをインストール
/plugin install fable-team@fable-team

# 3. 対象プロジェクトで導入(状態ディレクトリ作成 + CLAUDE.md への規約組み込み)
/fable-team:init
```

## アップデート

```
# 1. マーケットプレイス情報を更新
/plugin marketplace update fable-team

# 2. インストール済みプラグインを更新
/plugin update fable-team@fable-team

# 3. 導入済みの各プロジェクトで init を再実行 —— リリースノートに規約(rules.md)の
#    変更が含まれる場合のみ必要。冪等: CLAUDE.md の fable-team マーカー間だけを置き換える
/fable-team:init
```

補足: サードパーティのマーケットプレイスは既定では自動更新されない。
`/plugin` → Marketplaces タブからマーケットプレイス単位で自動更新を有効化できる。

## クイックスタート

```
1. メインセッションを Opus にする      /model opus
2. 単発タスク(1 セッション完結)      /fable-team:task ○○を修正して
3. 長期ミッションを開始する            /fable-team:mission ○○を実装する
4. 実行ループを回す                    /fable-team:work
   (自動で回し続けるなら)             /loop /fable-team:work
5. セッションが切れた・翌日になった    新セッションで /fable-team:resume
6. ミッション完了後                    /fable-team:retro で知見を収穫
7. シグナルが溜まったら                /fable-team:grow でチーム自身を改善
```

単発タスクは `task`、セッションをまたぐ規模は `mission`。
迷ったら「明日も続きをやるか?」で判断する。**昇格はいつでもできる(降格はできない)。**

### どのパーミッションモードで始めるか

セッションの入口は**通常モード**でよい —— Plan Mode で始める必要はない。
着手(`task` / `mission`)自体が「偵察 → 計画 → 承認」のゲートを内蔵し、計画を
`plan.md` に永続化するため、Plan Mode を重ねると同じ計画を二度承認することになる。
さらに Plan Mode 中は着手が作る `.fable-team/` の状態ファイルを書けない。
計画承認後、委譲ループが回り始めたら編集自動承認に上げると噛み合う
(`/loop /fable-team:work` ではほぼ前提)。
Plan Mode が今も有効なのは 2 箇所:ミッション途中の大きな方針転換と、
フレームワーク外の生の編集で「編集されない保証」が欲しいとき。

## 構成

```
claude-fable-team/       ← Claude Plugin 本体(このリポジトリ)
├── .claude-plugin/
│   ├── plugin.json        マニフェスト
│   └── marketplace.json   セルフホストのマーケットプレイス定義
├── agents/              ← 専門サブエージェント 7 名
│   ├── architect.md       (Opus)   設計・計画
│   ├── debugger.md        (Opus)   難バグの根本原因分析
│   ├── reviewer.md        (Opus)   敵対的コードレビュー
│   ├── builder.md         (Sonnet) 実装・テスト作成
│   ├── verifier.md        (Sonnet) 動作検証(E2E)
│   ├── scout.md           (Haiku)  探索・調査(並列ファンアウト)
│   └── scribe.md          (Haiku)  チェックポイント・復旧記録
├── skills/              ← 導入 1 + ブレスト 1 + 単発 1 + ミッション 5 + 手筋 4 + 成長 1
│   ├── init/              プロジェクト導入(規約の正本 rules.md を同梱)
│   ├── brainstorm/        ミッション前のブレインストーミング:発散→収束、task/mission 着手用の goal/DoD を起草
│   ├── task/              単発タスクの遂行(1 セッション完結。昇格経路つき)
│   ├── mission/           ミッション開始(templates/ と記入例 example/ を同梱)
│   ├── work/              実行ループ(委譲→検証→記録。無人ループモードつき)
│   ├── checkpoint/        状態の凍結
│   ├── resume/            新セッションでの完全復帰
│   ├── retro/             完了後の知見収穫
│   ├── grow/              チーム自身の成長(シグナル蒸留→資産更新)
│   └── debug/ verify/ brief/ judge/   手筋スキル(各 playbook.md 同梱)
├── README.md / HANDOFF.md / CHANGELOG.md / CLAUDE.md(HQ 用)
└── .fable-team/         ← この HQ リポジトリ自身の状態(配布物ではない)
```

導入先プロジェクトに増えるのは 2 つだけ:
**`.fable-team/`**(ミッション状態と成長ループ)と **`.claude/skills/pj-*/`**(収穫された
プロジェクト固有スキル。プロジェクトを超えて使えるものは `~/.claude/skills/` へ卒業)。

## 設計思想(1 段落で)

Fable 5 の長期一貫性は「巨大な単一コンテキスト」で実現されていた。
Fable Team はそれを「`.fable-team/` ディレクトリへの規律ある状態外部化」で置き換える。
真実はコンテキストではなくファイルにあり、どのセッションもいつ死んでよい。
判断が必要な仕事は Opus に、量産は Sonnet に、幅と速度は Haiku に振り、
すべての成果は「観測可能な完了条件」と「動作検証」を通ってから完了になる。

## 開発(このリポジトリを育てる)

- フレームワークへの変更は承認制で、根拠シグナルつきで `CHANGELOG.md` に記録する
- 検証の手順: `claude plugin validate .` → ローカルインストール →
  実プロジェクトで `/fable-team:init` から一連の動作を確認する
- チェックポイントごとにコミットする(変更履歴がそのままチームの成長史になる)
