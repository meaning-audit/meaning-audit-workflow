# Finding Types v1.1

- Name: Finding Types
- Version: v1.1
- Status: RELEASED（v1.1、2026-10-09）
- Basis: Finding Types v1.0。Finding Type の一覧と定義は変更していない。記入先の欄の名前だけを Output Contract v1.1 に合わせた

Finding Type は、Finding Ledger で Meaning Shift の種類を記録するための運用ラベルです。新しい理論ではなく、Document Class ごとの重点観点（[../docs/document-classes-v1.1.md](../docs/document-classes-v1.1.md)）を、監査で使える名前に揃えたものです。

1 つの Finding に複数の種類が当てはまる場合は、主たる種類を 1 つ記録し、Content（必要なら Annotation）で補足します。Finding Type の欄に括弧書き・注記・複数の値を入れません。

---

| Finding Type | 何が起きているか | 主に関わる Stage | 主に関わる Class |
|---|---|---|---|
| SELECTION | Source の一部だけが選ばれ、選ばれなかった部分によって意味が変わる | Interpretation | A, B |
| COMPRESSION | 要約・圧縮の過程で、限定条件・範囲・例外・不確実性が消える | Interpretation | A, B |
| EVIDENCE_INTERPRETATION_BLUR | Evidence の記述と、作成者の解釈の境界が不明確 | Interpretation | B, C |
| QUOTE_HANDLING | 引用の切り取り・言い換え・帰属によって、発言者の意味が変わる | Interpretation | B |
| INFERENCE_GAP | 根拠から主張への推論に、示されていない前提（Warrant）がある | Inference / Warrant | B, C |
| CAUSAL_IMPLICATION | 相関・並置・時系列が、因果として提示・示唆される | Inference / Warrant | A, B, C |
| FRAMING | 見出し・順序・語彙・強調によって、意味づけが変わる | Context / Pragmatics | A, B |
| VISUAL_CLAIM | 図・グラフ・色・配置が、本文や Source 以上の主張をする（Visualization を含む） | Context / Pragmatics | A |
| NARRATIVE | 物語的構成・編集上の枠組みが、根拠にない意味を加える（Editorial framing を含む） | Context / Pragmatics | B |
| TITLE_BODY_GAP | タイトル・見出しと本文の主張の強さ・範囲が一致しない | Context / Pragmatics | B |
| CONTEXT_LOSS | 元の文脈・前提・対象読者が失われ、別の意味で読まれる | Context / Pragmatics | A, B |
| AMPLIFICATION | 確度・強度・範囲が、根拠より強く提示される（Meaning amplification） | Commitment | A, B, C |
| COMMITMENT_ESCALATION | 推論や可能性が、判断・結論・推奨として採用される | Commitment | C |
| OTHER | 上記のどれにも当てはまらない | — | — |

---

## OTHER の扱い

`OTHER` を使った場合は、

1. Content に、何が起きているかを具体的に書く（Finding Type の欄に括弧で書かない）
2. 新しい Finding Type を作らない
3. 繰り返し現れる場合は、[../tests/post-freeze-candidates.md](../tests/post-freeze-candidates.md) に候補として記録する

## Finding Type と Status の関係

Finding Type は「何が起きているか」、Status は「根拠によってどこまで支えられているか（Mode B では、どこまで追跡できるか）」を表します。両者は独立に記録します。

例: `COMPRESSION` が起きていても、圧縮後の主張が Source の範囲内に収まっていれば `SUPPORTED` になり得ます。
