# Fable Team

Fable 5 が引退した世界で、**Opus / Sonnet / Haiku の分業**により Fable 5 の
「長期タスクを最後まで完遂する能力」を再現するための Claude Code チーム構成。

Fable 5 本人による引き継ぎ資料は [HANDOFF.md](HANDOFF.md) にある。

## 構成

```
claude-fable-team/       ← 将来 Claude Plugin として公開する本体
├── README.md            ← このファイル
├── HANDOFF.md           ← Fable 5 引き継ぎ資料(原則・パターン・アンチパターン)
├── CHANGELOG.md         ← フレームワーク自体の変更履歴(何を・なぜ・効いたか)
├── CLAUDE.md            ← チーム運用規約(全セッションが自動で読む)
├── .claude/             ← フレームワーク(配布物。プラグイン化の対象)
│   ├── agents/            専門サブエージェント 7 名
│   │   ├── architect.md   (Opus)   設計・計画
│   │   ├── debugger.md    (Opus)   難バグの根本原因分析
│   │   ├── reviewer.md    (Opus)   敵対的コードレビュー
│   │   ├── builder.md     (Sonnet) 実装・テスト作成
│   │   ├── verifier.md    (Sonnet) 動作検証(E2E)
│   │   ├── scout.md       (Haiku)  探索・調査(並列ファンアウト)
│   │   └── scribe.md      (Haiku)  記録・状態更新
│   └── skills/            ミッション 5 + 手筋 4 + 成長 1 スキル
│       ├── fable-mission/     ミッション開始(templates/ と example/ を同梱)
│       ├── fable-work/        実行ループ(委譲→検証→記録)
│       ├── fable-checkpoint/  状態の凍結
│       ├── fable-resume/      新セッションでの完全復帰
│       ├── fable-retro/       完了後の知見収穫
│       ├── fable-grow/        チーム自身の成長(シグナル蒸留→資産更新)
│       ├── fable-debug/       デバッグ手筋(playbook.md 同梱)
│       ├── fable-verify/      検証手筋(playbook.md 同梱)
│       ├── fable-brief/       委譲手筋(playbook.md 同梱)
│       └── fable-judge/       判断手筋(playbook.md 同梱)
└── .fable-team/         ← 状態(プロジェクトごと・可変。配布物ではない)
    ├── missions/<slug>/   ミッション状態(mission/plan/state/journal の 4 ファイル)
    └── growth/
        ├── inbox.md         成長シグナルの受信箱(気づいたら 1 行)
        └── changelog.md     このプロジェクトの成長記録
```

収穫されたプロジェクト固有スキルは `.claude/skills/pj-*/` に作られる
(`fable-*` = フレームワーク、`pj-*` = プロジェクトの学び。汎用なら `~/.claude/skills/` へ卒業)。

## クイックスタート

```
1. メインセッションを Opus にする      /model opus
2. 長期ミッションを開始する            /fable-mission ○○を実装する
3. 実行ループを回す                    /fable-work
   (自動で回し続けるなら)             /loop /fable-work
4. セッションが切れた・翌日になった    新セッションで /fable-resume
5. ミッション完了後                    /fable-retro で知見を収穫
6. シグナルが溜まったら                /fable-grow でチーム自身を改善
```

単発〜数時間で終わるタスクは、既存の `/cc`(cc-orchestrator)をそのまま使う。
**セッションをまたぐ規模になったら Fable Team のミッションプロトコルに乗せる。**

## 設計思想(1 段落で)

Fable 5 の長期一貫性は「巨大な単一コンテキスト」で実現されていた。
Fable Team はそれを「`.fable-team/` ディレクトリへの規律ある状態外部化」で置き換える。
真実はコンテキストではなくファイルにあり、どのセッションもいつ死んでよい。
判断が必要な仕事は Opus に、量産は Sonnet に、幅と速度は Haiku に振り、
すべての成果は「観測可能な完了条件」と「動作検証」を通ってから完了になる。

## 推奨セットアップ

- このディレクトリを `git init` し、チェックポイントごとにコミットする
  (ミッション状態の履歴がそのまま作業履歴になる)
- 実際のプロジェクトで使う場合は `.claude/` と `CLAUDE.md` の規約部分をコピーする
  (プレイブック・テンプレートはスキルに同梱済みなので付いてくる)。
  状態(`.fable-team/`)と収穫スキル(`pj-*`)は各プロジェクトで自然に生まれる
- 将来はこのリポジトリを Claude Plugin として公開する予定。フレームワークは `.claude/` に
  自己完結しており、導入先プロジェクトに増えるのは `.fable-team/` と `pj-*` スキルだけ
