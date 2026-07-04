# Fable Team フレームワーク変更履歴(CHANGELOG)

> Fable Team 本体(規約の正本・エージェント・スキル・同梱プレイブック/テンプレート)への
> 変更を、**根拠シグナル**と**効果測定の方法**つきで記録する。
> 「なぜこの規則があるのか」の答えはここにある。答えられない規則は削除候補である。
> 各プロジェクトでの成長記録(pj-* スキルの収穫など)は、そのプロジェクトの
> `.fable-team/growth/changelog.md` に記録する。
> 変更が効いたかは /fable-team:retro が評価し、効いていなければ /fable-team:grow で書き直すか削る。
> (2026-07-03 のプラグイン化以前のエントリは、当時のスキル名 /fable-* のまま残している)
>
> **Language policy**: Entries from 2026-07-03 (i18n) onward are written in English with a
> one-line Japanese gist (要約). Earlier entries remain in Japanese — history is not rewritten.

---

## 2026-07-03 — チーム発足(Fable 5 による構築)

- **変更**: エージェント 7 名・ミッションスキル 5(mission/work/checkpoint/resume/retro)・
  テンプレート一式・HANDOFF.md・CLAUDE.md を作成
- **根拠**: Fable 5 引退に備えた引き継ぎ(ユーザー依頼)
- **効果測定**: 初回の実ミッションの /fable-retro で「プロトコルが回ったか・
  セッションまたぎの引き継ぎが機能したか」を評価する

## 2026-07-03 — プレイブック 4 冊と記入例ミッションを追加

- **変更**: playbooks/(debugging・verification・briefing・judgment)、
  missions/_example-todo-api/、debugger・verifier 定義への参照配線
- **根拠**: 構造(規約・役割)だけでは職人芸(手筋)が引き継げない(Fable 5 の判断)
- **効果測定**: 委譲ブリーフにプレイブックが実際に添付されているか、
  同種の手戻りが減るかを retro で見る

## 2026-07-03 — 手筋スキル 4 つを追加(/fable-debug・verify・brief・judge)

- **変更**: プレイブックの起動装置としての薄いラッパースキル。本文は複製せず、
  単一の真実をプレイブック側に維持
- **根拠**: ユーザー指摘「プレイブックは Skills にできるのではないか」(**修正シグナル**)
- **効果測定**: 指揮者が該当場面で自発的にスキルを起動しているかを retro で見る

## 2026-07-03 — 成長ループを実装(growth/ + /fable-grow)

- **変更**: growth/inbox.md・growth/changelog.md・/fable-grow スキルを新設。
  CLAUDE.md に「成長ループ」節、fable-work にシグナル捕獲、fable-retro に効果検証と
  蒸留の委譲、scribe に inbox 追記の責務、HANDOFF.md に強み 5 を追記
- **根拠**: ユーザー依頼「Fable 5 の成長プロセス自体をチームに実装する」
- **効果測定**: 2〜3 ミッション後、inbox にシグナルが実際に溜まっているか(捕獲率)、
  /fable-grow が回って資産が更新されたかを評価する

## 2026-07-03 — プラグイン化を見据えた配置再編(.fable-team / pj-*)

- **変更**: プレイブックを各手筋スキルに `playbook.md` として同梱(`playbooks/` 廃止)、
  テンプレート・記入例を fable-mission に同梱(`missions/` 廃止)、可変状態を
  `.fable-team/`(missions + growth)へ一本化。changelog を二層に分離 ——
  フレームワークは本ファイル、プロジェクトの学びは `.fable-team/growth/changelog.md`。
  収穫スキルは `pj-*` として `.claude/skills/` に作成し、汎用なら `~/.claude/skills/` へ
  卒業する 2 段階に
- **根拠**: ユーザーの修正シグナル「Claude Plugin として公開したい。ユーザーのディレクトリを
  広く使わず、収穫物は /pj-* に」。配布物(読み取り専用)と状態(可変)の分離原則で応答
- **効果測定**: プラグイン化作業時にこの分離のまま移行できるか。導入先プロジェクトに
  増えるものが `.fable-team/` と `pj-*` スキルだけに収まっているか

## 2026-07-03 — ハーネス工学・ループ工学の取り込み

- **変更**: ①検証ハーネスの明示化 —— fable-mission の偵察に必須角度「検証ハーネス」を追加、
  mission.md テンプレートに「検証ハーネス」節を新設(記入例にも反映)、fable-work のブリーフ
  必須項目と briefing playbook に「ハーネスを毎回渡す」を追記 ②fable-work に「無人ループ
  モード」の規律を新設(停止条件・停滞検知・git コミットとセット・停止時の置き土産)
  ③HANDOFF の失敗パターン集に「検証が弱いまま無人ループ」、機能マップに Workflow を追記
- **根拠**: ユーザーシグナル「ハーネスエンジニアリング・ループエンジニアリングは組み込む
  価値があるか検討して」。検討の結論 —— ループは速さを増幅するが正しさは増幅しない。
  正しさを担うハーネスの明示化を先に、無人ループ規律をその上に載せた。
  hooks の前倒し導入は見送り(証拠が出てから格上げする現行方針を維持)
- **効果測定**: builder / verifier がハーネスの再発見に時間を使っていないか、
  無人 /loop 走行が停滞せず適切な停止点で止まるかを retro で見る

## 2026-07-03 — 単発タスクスキル /fable-task を追加(cc-orchestrator 依存の解消)

- **変更**: 1 セッションで完結する単発タスクの受け口 `/fable-task` を新設
  (重量判定 → 分解と完了条件 → 委譲ループ → 検証ゲート → 報告。ミッションへの
  昇格経路つき)。CLAUDE.md の「関連システム」を「タスクの受け口(規模ルーティング)」に
  書き換え、fable-mission・fable-grow・README・HANDOFF から /cc への依存参照を除去
- **根拠**: ユーザー依頼「小規模タスクも Fable Team で完結させる」。
  設計方針 —— ミッションの重装備(状態ファイル)は省き、品質規律(委譲・検証・
  正直な報告)は省かない。承認ゲートは常時提示型ではなく「不可逆・外部公開・
  解釈が割れる場合のみ」に軽量化(Fable 5 の実運用と同じ)
- **効果測定**: 単発タスクが検証ゲートを通っているか、ミッション級の取り違え
  (昇格の遅れ)が起きていないかを retro で見る

## 2026-07-03 — Claude Plugin 化(v0.1.0)

- **変更**: `.claude-plugin/`(plugin.json + marketplace.json)を新設し、`agents/` と
  `skills/` をプラグインルート直下へ移動。スキル名から fable- 接頭辞を除去
  (プラグインスキルの呼び出しは完全修飾が強制されるため `/fable-team:task` 形式に)。
  導入スキル `init` を新設 —— 規約の正本 `rules.md` と状態ファイルテンプレートを同梱し、
  マーカー方式(fable-team:rules:start/end)で対象プロジェクトの CLAUDE.md を冪等に更新する。
  HQ の CLAUDE.md は `@skills/init/rules.md` のインポート + HQ 固有規約の薄い構成に。
  同梱リソースの参照は `${CLAUDE_PLUGIN_ROOT}` 変数に統一
- **根拠**: ユーザー依頼「Claude Plugin 化して」。命名は選択肢を提示し、
  fable-team:task 形式をユーザーが選択。プラグイン仕様(完全修飾の強制・コンポーネントの
  ルート直下配置・CLAUDE.md の @import・validate CLI)は公式ドキュメントで検証してから実装
- **効果測定**: `claude plugin validate .` が通ること。ローカルインストール →
  /fable-team:init → /fable-team:task の一連が実プロジェクトで動くことを次の retro で確認

## 2026-07-03 — English-ization and public release (i18n-publish mission)

> 要約(gist): フレームワーク内部を英語化し 3 層言語設計を導入。逆翻訳レビューが状態値の割れと
> resume の grep 指示先という設計欠陥 2 件を修正。二か国語ドキュメント + MIT LICENSE + v0.1.0 を公開。
> retro で落とし穴「翻訳=設計レビュー」を追加(発注者承認)。

- **Change**:
  - Translated the framework internals (agents/, skills/, rules.md, playbooks, templates, manifests) to
    English under a **3-layer language design**: internals = English; runtime interaction and mission state
    files = the user's language (new `## Language` rule in rules.md); docs = bilingual (README/HANDOFF in
    en + ja, with HANDOFF.ja.md authoritative).
  - Two design fixes surfaced by the back-translation review, beyond mere translation: **unified the status
    tokens** to `in progress` / `completed` / `aborted` (previously split completed=done/completed and
    aborted=aborted/paused), and **fixed the resume grep target** to the `Status:` line in mission.md (it had
    pointed at state.md, which held only by a Japanese-heading coincidence).
  - Added bilingual README/HANDOFF with cross-links, a MIT `LICENSE`, and published to
    `rabitarochan/claude-fable-team` (public, v0.1.0).
  - **Pitfall added (retro, owner-approved A)**: "Treating translation as word substitution" — an i18n pass
    doubles as a design review; budget for design fixes from the start (HANDOFF §7).
- **Evidence signal**: owner request "publish on GitHub, in English, but I don't read English." The
  back-translation review is the mechanism that let a non-English-reading owner accept English deliverables.
- **Effectiveness measure**: the back-translation review found 14 fixes + 2 design flaws (it worked). Next
  retro: confirm the bilingual docs don't drift (English is authoritative) and that the status-token / grep-
  target fixes hold across resumes.

## 2026-07-04 — Add /fable-team:brainstorm skill (brainstorm-asset mission)

> 要約(gist): ミッション前のブレインストーミング支援スキル /fable-team:brainstorm を新設。ゴールがあいまいな段階で「枠づけ→発散→収束→goal/DoD 草案化」を回し、task/mission の intake に接続する。

- **Change**: New `skills/brainstorm/SKILL.md` — a single-file command skill (sibling of `task`): procedure (problem framing → divergence → convergence → goal/DoD drafting → intake routing), a 6-lens starter catalog, a fenced "Brainstorm Summary" output block that feeds /fable-team:task or /fable-team:mission intake, divergence fan-out pinned to Opus-tier agents (architect) with scoring/merging kept by the Conductor (HANDOFF §5 Judge Panel reuse), and the user-language dialogue rule. README.md and README.ja.md structure trees + counting lines updated. Deliberately NOT added: a new agent, a playbook.md, templates/, state directories, rules.md changes (so no re-init propagation to consuming projects is needed).
- **Evidence signal**: The user explicitly asked whether the Fable 5 handoff includes brainstorming (pre-project ideation) support; a repo-wide search found none (closest: the Judge Panel orchestration pattern in HANDOFF §5). Dogfooded within the same mission: a real Japanese-language brainstorm on 2 unprocessed growth-inbox signals produced a summary the verifier judged intake-fit without rework (PASS-WITH-NOTES). Adversarial review (Opus) at the Phase 1 gate: APPROVE-WITH-FIXES, all findings resolved in one cycle.
- **Effectiveness measure**: To evaluate at future /fable-team:retro / /fable-team:grow: (1) brainstorm summaries continue to be adopted by task/mission intake without rework; (2) discoverability — the skill actually gets proposed when a fuzzy-goal request arrives (rules.md intake section was intentionally left unchanged; recurring "should have brainstormed first" moments would be the signal to revisit); (3) the single-file/no-agent scope holds (reconsider-if conditions recorded in the mission plan).

## 2026-07-04 — Brainstorm convergence must confront recorded objections (brainstorm-asset retro)

> 要約(gist): ブレストの収束時、記録済みの反対意見と矛盾する案を選ぶ場合は、その意見を提示した上で覆す理由を記録するルールを収束ステップに1行追加。

- **Change**: One sub-bullet added to Step 3 (Convergence) of skills/brainstorm/SKILL.md requiring recorded objections (growth-inbox notes, journal decisions) to be surfaced and the override rationale recorded before converging.
- **Evidence signal**: During the brainstorm-asset dogfooding, the converged choice A2 (give scribe Bash) silently contradicted the growth-inbox note "Bash 付与は過剰"; the verifier flagged the unexplained contradiction (2.2 PASS-WITH-NOTES) and the user withdrew A2 at change-set approval — one avoidable approval cycle. Distilled at the 2026-07-04 retro from a 修正 (user-correction) signal and a 摩擦 signal.
- **Effectiveness measure**: At the next retro, check whether brainstorm summaries produced since then either contain no contradictions with recorded positions or explicitly state the overridden objection and rationale; zero repeat of a post-approval reversal caused by an unsurfaced objection.
