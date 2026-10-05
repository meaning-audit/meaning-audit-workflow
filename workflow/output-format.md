# Output Format: Meaning Audit Report v1.0

v1.0 の標準成果物は Meaning Audit Report です。以下の 13 セクションを、この順序で必ず含めます。該当する内容が無いセクションも省略せず、「該当なし」と書きます。

プロンプト（`prompts/`）に埋め込まれたテンプレートは、この文書を正とします。

---

## テンプレート

```markdown
# Meaning Audit Report

- Workflow version: Meaning Audit Workflow v1.0
- Prompt: <使用したプロンプトのファイル名>
- Auditor: <AI モデル名 / 人間の監査者名>
- Date: <YYYY-MM-DD>
- Review status: Human Review 未実施

## 1. Audit Object

| 項目 | 内容 |
|---|---|
| 名称 | |
| 形式 | |
| 作成者 / 生成元 | |
| 作成日 | |
| 監査範囲 | |

## 2. Audit Mode

- Mode: <Mode A: Source-Grounded Audit / Mode B: Artifact-Only Audit>
- 判定理由:
- （Mode B の場合）Source verification は実施できない。外部 Evidence がないため、本 Report は成果物内部の Traceability のみを判定し、誤りの断定は行わない。

## 3. Document Class

- Class: <A / B / C>（副次 Class があれば併記）
- 判定理由:
- 重点観点:

## 4. Audit Purpose

- 目的:
- （指定がなかった場合）既定値「Meaning Shift の所在を明らかにする」を使用した。

## 5. Evidence Boundary

| 区分 | 内容 |
|---|---|
| 参照した Source | |
| 参照できなかった Source | |
| 監査対象の範囲 | |
| 監査者が持ち込んだ外部知識 | なし / あり（該当 Finding:） |

## 6. Overall Finding

<3〜6 文。どこで、どのような Meaning Shift が起きているかの要約。点数・等級・ランキングは付けない。>

## 7. Key Meaning Shifts

| # | Meaning Unit | Shift の内容 | Stage | Finding |
|---|---|---|---|---|
| KS-1 | MU-xx | | | F-xx |

## 8. Meaning Trace

### KS-1: <短い名前>

| Stage | Trace |
|---|---|
| Evidence / Source | |
| Interpretation | |
| Inference / Warrant | |
| Context / Pragmatics | |
| Commitment / Presented Meaning | |
| Finding | |
| Status | |

（Key Meaning Shift ごとに繰り返す）

## 9. Finding Ledger

| ID | Meaning Unit | Location | Stage | Finding Type | 内容 | Status | 情報状態 | 根拠 |
|---|---|---|---|---|---|---|---|---|
| F-01 | MU-xx | | | | | | | |

## 10. Critical Unknowns

| # | Unknown | 影響する Finding | なぜ判定に重要か |
|---|---|---|---|
| U-1 | | | |

## 11. Source Verification Required

| # | 確認すべき Source / 事実 | 対象 Meaning Unit | 確認方法の候補 |
|---|---|---|---|
| SV-1 | | | |

## 12. Human Review Required

| # | 対象 Finding | レビューで確認すべき問い | Human Decision |
|---|---|---|---|
| HR-1 | F-xx | | （人間が記入: accept / revise / investigate / hold / reject / no action） |

## 13. Limitations

- 
```

---

## 各セクションの記入規則

### 1. Audit Object

分からない項目は推測で埋めず `UNKNOWN` と書きます。

### 2. Audit Mode

Mode B の場合、「Source verification は実施できない」旨を必ず書きます。Source が一部だけ提供されている場合は Mode A とし、Source の無い範囲を Evidence Boundary と Source Verification Required に書きます。

### 5. Evidence Boundary

監査者（AI）が自身の一般知識を判定に使った場合は、「あり」とし、該当 Finding を列挙します。外部知識による判定は、情報状態を `INFERRED` とします。

### 6. Overall Finding

- 点数・等級・ランキング・「良い／悪い」の総合評価は書きません
- Mode B では「誤り」「虚偽」「不正確」と断定しません

### 7. Key Meaning Shifts

すべての Finding ではなく、監査目的に照らして重要なものを選びます。目安は 3〜7 件です。

### 8. Meaning Trace

Meaning Trace は標準成果物です。Key Meaning Shift ごとに 1 表を作ります。

| Stage | 記入内容 |
|---|---|
| Evidence / Source | Mode A: Source の該当箇所と、Source が言っていること。Mode B: 成果物内で根拠として示されているもの（外部 Source は無いことを明記） |
| Interpretation | 根拠がどう読まれ、何が選ばれ・落とされたか |
| Inference / Warrant | どんな推論が使われたか。Warrant は明示されているか（監査者が補った場合は `INFERRED`） |
| Context / Pragmatics | 見出し・配置・図・語彙・想定読者によって、意味がどう変わるか |
| Commitment / Presented Meaning | 最終的に提示された Meaning と、その強さ（断定 / 推奨 / 可能性 / 留保付き） |
| Finding | 対応する Finding ID と要約 |
| Status | Mode A: SUPPORTED / PARTIALLY SUPPORTED / UNSUPPORTED / UNKNOWN。Mode B: TRACEABLE / PARTIALLY TRACEABLE / UNTRACEABLE / UNKNOWN |

該当する変化がない Stage は「変化なし」と書き、空欄にしません。確認できない Stage は `UNKNOWN` と書きます。

### 9. Finding Ledger

| 列 | 記入内容 |
|---|---|
| ID | `F-01` から連番 |
| Meaning Unit | STEP 1 の ID |
| Location | ページ・スライド・段落など |
| Stage | Meaning Shift が起きた Stage（Evidence / Source、Interpretation、Inference / Warrant、Context / Pragmatics、Commitment） |
| Finding Type | [finding-types.md](finding-types.md) の種別 |
| 内容 | 何が起きているかを 1〜2 文で。修正案は書かない |
| Status | Mode に対応した Status |
| 情報状態 | KNOWN / INFERRED / UNKNOWN / CONFLICTING |
| 根拠 | Source の箇所、または成果物内の箇所 |

### 10. Critical Unknowns

判定結果を左右する Unknown だけを書きます。Unknown を埋めるための推測は書きません。

### 11. Source Verification Required

Mode B では、Traceability の判定とは別に、元資料と照合すべき主張をここに挙げます。

### 12. Human Review Required

- AI は「レビューで確認すべき問い」まで書きます
- Human Decision 列は空欄のまま出力します（AI が選ばない）

### 13. Limitations

最低限、以下を確認して該当するものを書きます。

- Evidence Boundary の外側にある範囲
- AI が読めなかった要素（画像、図、表、PDF のレイアウトなど）
- Meaning Unit として抽出しなかった範囲
- 監査者の外部知識に依存した判定
- 監査が AI のみで行われ、Human Review 前であること
