# 現在地(state): 英語化と GitHub 公開

> **このファイルが唯一の真実。** セッションはいつ死んでもよい。

- slug: `i18n-publish`
- フェーズ: Phase 4 — 進行中(4.2 公開 / 4.3 タグ 完了、残 4.4 導入テストのみ)
- 進捗: 完了 17 / 全 18 タスク(Phase 1〜4.3 完了、残 4.4 のみ)
- 最終更新: 2026-07-03
- 更新者: 指揮者(resume セッション)

## 次の一手(最重要)

**発注者による 4.4 導入テスト待ち。**

別の実プロジェクトで新規 Claude Code セッションを開き、以下を実行:

(1) `/plugin marketplace add rabitarochan/claude-fable-team` — 公開リポジトリを marketplace に追加  
(2) `/plugin install fable-team@fable-team` — プラグインをインストール  
(3) `/fable-team:init` — ミッション環境を初期化

**完走条件:**
- init が例外なく完走し、`.fable-team/` ディレクトリが生成される
- `CLAUDE.md` に Fable Team 規約が埋め込まれている
- **日本語で対話される**(フレームワークがユーザー言語ルールを守っているか確認)

**完走したら:**  
DoD 全項目達成 → 本ミッションを `Status: completed` に変更 → `/fable-team:retro` を実行

## 進行中・中断点

なし(Phase 3 成果はコミット済み、ゲート待ち)。

## 検証状態

- 検証済み:
  - フレームワーク内部の英語化 — 日本語残存 grep 0(agents/skills/.claude-plugin)、`claude plugin validate .` 通過、逆翻訳レビュー 3 体の must-fix/recommended 全対応、状態トークン横断統一
  - gh 認証(rabitarochan、repo スコープ有)、翻訳対象規模 agents 7 / skills 28 の baseline 確認
  - 4.1 総合検証 — 日本語残存 0 / validate / 英日相互リンク / LICENSE=MIT rabitarochan / 言語規則 / 英語版本文クリーン の全 6 項目 green「公開可」
  - GitHub 公開 — リポジトリ public 作成成功 / main + v0.1.0 タグ push 成功 / `gh repo view` が visibility=PUBLIC 返却で確認
- 未検証: Phase 4.4 導入テスト(公開版の marketplace add → install → init 一連、実プロジェクトでの実行)

## ブロッカー・注意

- ※ セッションによりロール実行手段が変わる。resume 時に再確認すること。本セッションでは fable-team:* 専用エージェント(verifier 等)が利用可能
- 発注者は英語レビューをしない。承認・検収はすべて日本語で成立させること(逆翻訳レビュー必須)
- **今後の公開/クローン時の注意**: `gh repo create --public --source=. --push` は origin を SSH(git@github.com)で張るため、SSH エージェント署名が失敗する環境では初回 push が失敗する。対処は remote を HTTPS に手動 set-url した上で `gh auth setup-git` を実行すること。今後の公開手順に「HTTPS remote を使う」を織り込むべき
