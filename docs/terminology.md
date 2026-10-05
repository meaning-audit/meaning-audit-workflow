# Terminology

v1.0 で使う用語です。用語の追加は Human Review を経て行います。

## 構造

| 用語 | 定義 |
|---|---|
| Evidence / Source | 成果物の元になった資料・データ・証拠。Mode B では外部 Source は無く、成果物内で根拠として示されたものを扱う |
| Interpretation | Evidence / Source を読み、選び、まとめること |
| Inference / Warrant | 解釈から主張・結論へ進む推論と、根拠と結論をつなぐ理由 |
| Context / Pragmatics | 見出し・配置・語彙・図・想定読者など、表現の置かれ方によって生じる意味。v1.0 では Audience / Context と同じ STEP で扱う（概念上は分離） |
| Commitment | 成果物がある Meaning を判断・結論・推奨として採用すること |
| Integration | 各 STEP の結果を Report にまとめること |
| Human Review | 人間が Finding ごとの対応を決めること |

## 監査の単位と記録

| 用語 | 定義 |
|---|---|
| Audit Object | 監査対象の成果物 |
| Audit Purpose | 監査の目的。指定が無い場合の既定値は「Meaning Shift の所在を明らかにする」 |
| Evidence Boundary | 監査で参照した範囲と、参照していない範囲の境界 |
| Meaning Unit | 監査の単位となる、意味を担う主張・表現（`MU-01`〜） |
| Meaning Shift | 根拠から提示された Meaning までの間で、意味が加わる・変形される・強められる・弱められる・採用されること |
| Key Meaning Shift | 監査目的に照らして重要な Meaning Shift（`KS-1`〜） |
| Meaning Trace | 1 つの Key Meaning Shift を、Stage ごとに追跡した表 |
| Finding | 監査で記録する個別の指摘（`F-01`〜） |
| Finding Ledger | すべての Finding の一覧表 |
| Finding Type | Finding の種類を表す運用ラベル（[../workflow/finding-types.md](../workflow/finding-types.md)） |
| Critical Unknown | 判定結果を左右する Unknown |
| Source Verification Required | 元資料との照合が必要な主張の一覧 |
| Human Review Required | 人間の判断が必要な Finding と、確認すべき問いの一覧 |

## 監査モードと Status

| 用語 | 定義 |
|---|---|
| Mode A: Source-Grounded Audit | 元資料と照合する監査 |
| Mode B: Artifact-Only Audit | 成果物だけで行う監査。元資料への忠実性は判定しない |
| SUPPORTED / PARTIALLY SUPPORTED / UNSUPPORTED / UNKNOWN | Mode A の Status |
| TRACEABLE / PARTIALLY TRACEABLE / UNTRACEABLE / UNKNOWN | Mode B の Status |

定義の詳細は [../workflow/meaning-audit-workflow-v1.0.md](../workflow/meaning-audit-workflow-v1.0.md) の STEP 7。

## 情報状態

| 用語 | 定義 |
|---|---|
| KNOWN | 利用可能な資料で直接確認できる |
| INFERRED | 監査者の推論による |
| UNKNOWN | 利用可能な資料では分からない |
| CONFLICTING | 資料同士、または資料と成果物が食い違う |

## Human Decision

| 用語 | 定義 |
|---|---|
| accept | Finding を妥当と認める |
| revise | Finding の内容・Status・種類を修正する |
| investigate | 追加の確認を行う |
| hold | 現時点では判断しない |
| reject | Finding を妥当でないと判断する |
| no action | Finding は妥当だが対応は不要と判断する |
