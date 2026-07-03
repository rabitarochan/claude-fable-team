# このプロジェクトの成長記録(changelog)

> このプロジェクトで /fable-team:grow・/fable-team:retro が行った改善 —— `pj-*` スキルの収穫、
> プロジェクト規約の追加、シグナルの破棄 —— を、根拠と効果測定つきで記録する。
> Fable Team フレームワーク自体への変更は、フレームワークのリポジトリの `CHANGELOG.md` へ。
> 変更が効いたかは次の /fable-team:retro が評価し、効いていなければ /fable-team:grow で書き直すか削る。

---

## 2026-07-03 — i18n-publish retro:初の実ミッションでフレームワークを実証

- **記録**: 発足後初の実ミッション `i18n-publish` がエンドツーエンドで成功。過去変更の効果検証 ——
  ①ミッションプロトコル(4 状態ファイル)は**別セッションからの resume を state.md のみで成立**させ実証
  ②成長ループは作業中に 2 シグナル捕獲で稼働 ③検証ハーネス明示化は 4.1 で verifier が再発見コストゼロで検証
  ④委譲ブリーフは全 subagent が結論返答・ダンプなし。**壊れた/不発の変更はなし。** 無人ループ規律のみ未行使
- **署名的パターン(再利用候補)**: 逆翻訳レビュー —— glossary でアフォリズムを定訳固定 → 並列翻訳 →
  英→日に訳し戻して原文突合。英語を読まない発注者が英語成果物を検収できた唯一の方法。並列翻訳で用語割れゼロ
- **根拠**: 本ミッションの journal(resume 成功・4.1 オールグリーン・逆翻訳レビューが設計欠陥 2 件を露出)
- **効果測定**: 次ミッションでも resume が files-only で成立するか、inbox 捕獲が継続するかを次 retro で見る

## 2026-07-03 — 公開手順の環境知見:初回 push は HTTPS remote で

- **記録**: `gh repo create --public --source=. --push` は origin を SSH(git@github.com)で張るため、
  SSH 署名不可の環境では初回 push が失敗する。対処 = `git remote set-url origin https://github.com/<owner>/<repo>.git`
  → `gh auth setup-git` → `git push -u origin main`
- **根拠**: i18n-publish タスク 4.2 で実際に失敗し、上記手順で解決(journal 2026-07-03 GitHub 公開実行の項)
- **効果測定**: 次回の公開/クローン作業でこの手順により初回 push が一発で通るか

<!-- 承認待ちのフレームワーク変更提案(2026-07-03 retro 由来。承認後 Fable Team リポジトリの CHANGELOG.md へ):
  (1) HANDOFF.md 落とし穴カタログに「翻訳/i18n は設計レビューを兼ねる」を追加
  (2) resume スキル原則に「state.md のセッション固有前提は『セッション固有』と明記し resume 時に再確認」を追加
  (3) mission.md DoD の「skills 全 28」を実数(直下 12 / 対象 37 ファイル)に訂正 -->

