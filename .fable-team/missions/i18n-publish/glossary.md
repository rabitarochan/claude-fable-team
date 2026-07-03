# 翻訳用語集(glossary)— i18n-publish

> すべての翻訳担当はこの対訳に**厳密に**従う。ここにない用語で迷ったら、
> 勝手に決めずに指揮者へ返す(用語の揺れは逆翻訳レビューで検出・差し戻しになる)。

## 訳さない語(そのまま使う)

Fable Team / Fable 5 / Opus / Sonnet / Haiku / SkDD / pj-* / slug /
architect / builder / debugger / reviewer / verifier / scout / scribe(ロール名)/
inbox / changelog / journal / brief(ファイル・概念名として定着済みの英語)

## 中核概念

| 日本語 | 英語 | 備考 |
|---|---|---|
| 指揮者 | Conductor | メインセッションの役割 |
| ミッション | mission | |
| 単発タスク | one-shot task | 「1 セッション完結」は single-session |
| 手筋 | playbook | 手筋スキル = playbook skills |
| 委譲 | delegation / delegate | |
| ブリーフ | brief | 5 要素 = the five elements |
| 偵察 | recon | 偵察ファンアウト = scout fan-out |
| 検証ハーネス | verification harness | |
| 検証ゲート | verification gate | |
| 完了の定義 | Definition of Done (DoD) | |
| 観測可能な完了条件 | observable completion criteria | |
| 敵対的レビュー | adversarial review | |
| 状態の外部化 | externalizing state / externalized state | |
| 次の一手 | next move | state.md の最重要欄 |
| 現在地 | current state | state.md の見出し |
| 作業日誌 | work journal | ファイル名は journal.md |
| チェックポイント | checkpoint | |
| 引き継ぎ | handoff | |
| フェーズ境界 | phase boundary | |
| 昇格 / 降格 | promote / demote | |
| 重量判定 | weight-class triage | 軽量/中量/ミッション級 = light / medium / mission-class |
| 無人ループモード | unattended loop mode | |
| 停滞検知 | stall detection | |
| 停止時の置き土産 | parting notes | |

## 成長ループ関連

| 日本語 | 英語 | 備考 |
|---|---|---|
| 成長ループ | growth loop | |
| 成長シグナル | growth signal | |
| 捕獲 | capture | |
| 蒸留 | distill / distillation | |
| 収穫 | harvest | SkDD の Harvest と対応 |
| 卒業(user レベルへ) | graduate / graduation | |
| 落とし先 | destination (layer) | |
| ルールダイエット | rule diet | |
| 3 回ルール | rule of three | |
| 効果測定 | effectiveness check | changelog の欄名 |
| 破棄も立派な処理 | Discarding is a valid outcome. | |

## 決まり文句(アフォリズム)— 一字一句この訳で統一

| 日本語 | 英語 |
|---|---|
| 肥大化は死 | Bloat is death. |
| テスト green ≠ 動く | Green tests ≠ working software. |
| 記憶よりファイル | Files over memory. |
| 現実が真実 | Reality is the truth. |
| 次のセッションの自分は他人 | Your next session is a stranger. |
| セッションはいつ死んでもよい | Any session may die at any moment. |
| 分析はしない、捕獲だけ | Don't analyze — just capture. |
| 昇格はいつでもできる(降格はできない) | You can always promote; you can never demote. |
| 変えっぱなしは成長ではない | Changing things isn't growth unless you check they worked. |
| 「次からは気をつける」は成長ではない。仕組みに落ちて初めて成長である | "I'll be careful next time" is not growth. It becomes growth only when it lands in the system. |
| ループは速さを増幅するが、正しさは増幅しない | Loops amplify speed, not correctness. |
| ハーネスが先、ループはその上に | Harness first; loops on top. |
| 記録されていない進捗は、存在しない進捗である | Unrecorded progress is no progress. |
| 明日も続きをやるか? | Will you continue this tomorrow? |
| 轍(失敗パターン集) | pitfalls (the pitfall catalog) |

## 文体規則

- SKILL.md / agents は**簡潔な命令形**(You are... / Do X. / Never Y.)。冗長な敬語調にしない
- 見出し・表・状態記号(⬜ 🔄 ✅ ⏸️)・コードブロック・パスは構造を変えない
- 決まり文句は文中でも上記の定訳を崩さない(意訳禁止)
- 「発注者」「ユーザー」は一律 the user
