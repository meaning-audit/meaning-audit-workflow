# Principles

Meaning Audit Workflow v1.0 の運用原則です。新しい理論ではなく、Workflow を実行するときに守る約束事をまとめています。

## 1. 次の理論を書く前に、今の理論を動かす

v1.0 の目的は、Meaning Audit を実際の文書で動かし、テストし、修正できる状態にすることです。新しい概念が必要に見えても、仕様に直接採用せず [../tests/post-freeze-candidates.md](../tests/post-freeze-candidates.md) に記録します。

## 2. 意味の変化を追跡する

Meaning Audit が追跡するのは、Evidence / Source から最終的に提示された Meaning までの間で、

- どこで意味が加わったか
- どこで変形されたか
- どこで推論されたか
- どこで判断として採用されたか

です。成果物の良し悪しを採点することではありません。

## 3. AI は追跡し、人間が判断する

AI の役割は trace / expose / question / classify です。Human の役割は accept / revise / investigate / hold / reject / no action です。監査は AI だけで完結させません。

## 4. Evidence Boundary を明示する

何を見て、何を見ていないかを、必ず書きます。境界の外側については判定しません。

## 5. Unknown は欠陥ではなく情報状態である

情報状態は KNOWN / INFERRED / UNKNOWN / CONFLICTING で記録します。UNKNOWN を、もっともらしい推測を経て事実に変えてはなりません。

## 6. 元資料が無いときは、誤りと断定しない

Artifact-Only Audit では、成果物の内部での Traceability だけを判定します。外部 Evidence なしに「誤り」と断定しません。

## 7. 書き直さない・決めない

v1.0 は、自動 Rewrite、自動意思決定、スコアリング、ランキングを行いません。
