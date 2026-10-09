# Migration Guide: v1.0 → v1.1

v1.0 の Meaning Audit を使っていた人が、v1.1 に移るときの要点です。v1.0 の文書は削除していないので、v1.0 の Report を読む・比べるときは v1.0 の文書を使えます。自動の移行ツールはありません。

## 1. 使う文書

| 用途 | v1.0 | v1.1 |
|---|---|---|
| Workflow | [workflow/meaning-audit-workflow-v1.0.md](../workflow/meaning-audit-workflow-v1.0.md) | [workflow/meaning-audit-workflow-v1.1.md](../workflow/meaning-audit-workflow-v1.1.md) |
| Report の形式 | [workflow/output-format.md](../workflow/output-format.md)（13 セクション） | [workflow/meaning-audit-output-contract-v1.1.md](../workflow/meaning-audit-output-contract-v1.1.md)（ヘッダー＋ 14 セクション） |
| Prompt | [minimum-audit-v1.0](../prompts/minimum-audit-v1.0.md)、Mode 別の 2 つ | [minimum-audit-v1.1](../prompts/minimum-audit-v1.1.md) の 1 つだけ |
| Skill の実行規則 | （SKILL.md のみ） | [runtime/meaning-audit-runtime-validation-v1.1.md](../runtime/meaning-audit-runtime-validation-v1.1.md) |
| 補助文書 | 版なしの名前（`docs/audit-modes.md` など） | `-v1.1` 付きの名前（`docs/audit-modes-v1.1.md` など） |

## 2. 変わった点

| 項目 | v1.0 | v1.1 |
|---|---|---|
| Document Class | 主たる Class に副次 Class を併記できた | Class の欄は Canonical の値 1 つだけ（A / B / C）。他の Class の性質は判定理由などの自由記述に書く |
| Meaning Units | Report に独立したセクションが無い | Report §8 に MU ID と内容を出す。Location と Primary Claim Type は任意。Finding は MU ID を 1 つ以上参照する |
| 情報状態 | Finding ごとに 1 つ（Finding Ledger の列） | Finding 単位の情報状態は廃止。判断に関係する要素ごとに 1 つ（Information State by Element）。必要な場合だけ部分に分ける |
| Report の構造 | 13 セクション | ヘッダー＋ §1〜§14。v1.0 の §8〜§13 は v1.1 の §9〜§14。Finding Ledger は §10.1 Finding Summary と §10.2 Finding Detail の 2 層 |
| Meaning Trace | 確認できない Stage を `UNKNOWN` と書けた | 情報状態を書かない。確立できない Stage は「Evidence Boundary の中で確立できない」などの説明の文で書く。Status 行の Status の値 `UNKNOWN` は使える |
| `UNKNOWN` | — | Evidence に基づいて選ぶ値で、判断の難しさで選ばない。意味は欄で決まる（情報状態、Status、Source Set Status、Location など）。元資料が一部だけの場合、見つからないことだけで `UNSUPPORTED` も `UNKNOWN` も決めない |
| 分類の欄 | 括弧書き・複合値が出ることがあった | 各欄に Canonical の値 1 つ。複合値・括弧書き・疑問符を入れない |
| Stage | Key Meaning Shifts の Stage 欄の書き方に規定が無かった | Primary Stage を 1 つ。複数の Stage にまたがる場合は Finding Detail の Stage Path に書く |
| Runtime Validation | なし | Skill は出力の前に VR-01〜VR-27 で検証し、結果を PASS / PASS WITH WARNING / FAIL で記録する |
| Runtime Record | なし | Skill は Report の後に実行と検証の記録を示す。Report のセクションではない |
| Skill パッケージ | `references/workflow.md`、`output-format.md`、`finding-types.md`、`limitations.md` | `references/workflow-v1.1.md`、`output-contract-v1.1.md`、`prompt-v1.1.md`、`runtime-validation-v1.1.md`、`finding-types.md`、`limitations.md` |
| Prompt | Mode 別の Prompt があった | v1.1 の Mode 別の Prompt は無い。`minimum-audit-v1.1` を Mode A・Mode B の両方に使い、Mode は Prompt の中で判定する |
| Prompt 欄（Report のヘッダー） | `minimum-audit-v1.0` など | 直接実行：`minimum-audit-v1.1`。Skill 実行：`skill: meaning-audit (minimum-audit-v1.1)` |

## 3. 移行の手順

1. **Skill を入れ直す。** 以前の `meaning-audit` フォルダを取り除いてから、v1.1 のフォルダをコピーする。上書きのコピーだけでは v1.0 の references が残る
2. **Prompt を直接使っている場合は、`minimum-audit-v1.1` に切り替える。** Mode A・Mode B のどちらにも同じ Prompt を使う
3. **Report を読む・書く道具や手順を、14 セクションと 2 層の Finding Ledger に合わせる。** v1.0 の Report は v1.0 の Output Format のまま読む
4. **v1.0 の Report を v1.1 の形式に移す必要がある場合は、Human が行う。** Finding 単位の情報状態（とくに `KNOWN / INFERRED` のような複合の値）を要素ごとの情報状態に移すには、解釈が要る。自動の変換はしない

## 4. 変わらない点

- STEP 0〜8、Mode A・Mode B、Mode ごとの Status の語彙、Finding Type 14 種、Human Decision の 6 つの値
- AI は Human Decision を選ばない。監査は Human Review で完了する
- 採点・書き直し・判断の代行をしない
- 同じ入力でも、Finding の数・まとめ方・Finding Type・Status は実行ごとに変わりうる
