# ミッション: 英語化と GitHub 公開(i18n-publish)

- slug: `i18n-publish`
- 開始日: 2026-07-03
- 状態: 完了(completed)— 2026-07-03(4.4 導入テスト完了により DoD 全達成)
- 発注者の依頼(原文のまま):
  > GitHub で公開したいけど、どうせなら広く使えるように英語化したい。ただ、私は日本人で英語が苦手なので、英語化して私が理解できるかは分からない・・・。
  > (方針相談の後)1 の英語化してから公開で。ミッションとして立ち上げて

## ゴール

Fable Team プラグインを **3 層言語設計**で英語化し、GitHub に公開する:

1. フレームワーク内部(skills / agents / rules / playbooks)= 英語
2. 実行時の対話と状態ファイル = ユーザーの言語(rules に規則を追加して保証)
3. ドキュメント = 二か国語(README.md 英 + README.ja.md 日、HANDOFF も同様)

**発注者は英語のレビューをしない。** 議論・承認・報告はすべて日本語で行い、
英語を書くのはチームの仕事とする。

## 完了の定義(Definition of Done)

- [x] フレームワーク内部(agents/ 全 7 ファイル、skills/ 配下 28 ファイル(12 スキル)、.claude-plugin/ の description)に
      日本語文字が残っていない(`[ぁ-んァ-ヶ一-龯]` の grep が 0 件)
- [x] rules.md に「ユーザーの言語で対話し、ミッション状態ファイルもユーザーの言語で書く」
      規則が入っている
- [x] 逆翻訳レビュー(英→日に訳し戻して原文と意味を突き合わせ)で、未対応の意味ドリフト指摘が 0 件
- [x] README.md(英)/ README.ja.md(日)、HANDOFF.md(英)/ HANDOFF.ja.md(日本語原本)が
      存在し、相互リンクされている
- [x] LICENSE(MIT)が存在する
- [x] `claude plugin validate .` が通る
- [x] GitHub の公開リポジトリ `rabitarochan/claude-fable-team` に push され、
      `/plugin marketplace add rabitarochan/claude-fable-team` → install → init の一連が動く

## 検証ハーネス(このプロジェクトのフィードバックループ)

| 装置 | コマンド | 所要時間の目安 |
|---|---|---|
| プラグイン検証 | `claude plugin validate .` | 約 2 秒 |
| 日本語残存チェック | `[ぁ-んァ-ヶ一-龯]` を agents/ skills/ .claude-plugin/ に grep | 数秒 |
| 意味ドリフト検査 | reviewer 役による逆翻訳レビュー(glossary 準拠チェック込み) | エージェント 1 回 |
| 公開確認 | `gh auth status`(確認済み: rabitarochan、repo スコープ有)/ `gh repo view` | 数秒 |

## 制約

- **意味のドリフト禁止**: 全訳文は逆翻訳レビューを通す。特にニュアンスの濃い箇所
  (「肥大化は死」「テスト green ≠ 動く」「昇格は可・降格は不可」等)は glossary で対訳を固定する
- 発注者への提示物(計画・承認・報告)はすべて日本語
- 英語が正、`.ja.md` は翻訳(ただし HANDOFF は日本語が原本、英語が翻訳)
- 公開先: `rabitarochan/claude-fable-team`(public)、ライセンスは MIT(plugin.json 記載済み)
- git 履歴は保持する(force push しない)

## スコープ外

- 英語以外の言語対応(仕組み上、実行時層は任意言語に自動対応する)
- ドキュメントサイト・GitHub Pages
- 公式マーケットプレイスへの登録申請(「後でやるかも」)
- CHANGELOG 過去エントリの英訳(歴史は日本語のまま残す)
