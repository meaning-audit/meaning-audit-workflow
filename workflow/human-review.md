# Human Review v1.0

Meaning Audit は AI だけで完結しません。STEP 8 の Human Review で、人間が Finding ごとの対応を決めて、初めて監査が完了します。

---

## 役割

| AI | Human |
|---|---|
| trace / expose / question / classify | accept / revise / investigate / hold / reject / no action |

AI は Human Decision を選びません。AI の出力に Human Decision が書かれていた場合、それは無効とし、人間が改めて決めます。

## Human Decision の定義

| Decision | 意味 | 次の行動の例 |
|---|---|---|
| accept | Finding を妥当と認め、成果物の問題として受け入れる | 成果物の修正・注記を検討する |
| revise | Finding の内容・Status・Finding Type を修正する | Finding Ledger を書き換え、理由を記録する |
| investigate | 判断に追加の確認が必要 | Source を確認する、作成者に問い合わせる |
| hold | 現時点では判断しない | 保留理由と再検討の条件を記録する |
| reject | Finding を妥当でないと判断する | 却下理由を記録する |
| no action | Finding は妥当だが、対応は不要と判断する | 不要と判断した理由を記録する |

`accept` は「Finding を受け入れる」という意味で、成果物の修正方法までは決めません。修正方法を決めるのは、Meaning Audit の外側の作業です。

## 手順

1. Report の Audit Mode と Evidence Boundary を確認する（Mode B なのに誤りと断定していないか）
2. Human Review Required の項目を順に確認する
3. Finding Ledger の残りの Finding を確認する
4. Critical Unknowns と Source Verification Required のうち、自分で確認できるものを確認する
5. Finding ごとに Human Decision を記録する
6. 監査全体についての所見を記録する
7. ワークフロー・プロンプトの不具合に気づいた場合は [../tests/failure-patterns.md](../tests/failure-patterns.md)、新しい概念が必要に見えた場合は [../tests/post-freeze-candidates.md](../tests/post-freeze-candidates.md) に記録する

## レビューで確認する観点

- UNKNOWN が、もっともらしい推測で埋められていないか
- INFERRED が、後の記述で事実（KNOWN）として扱われていないか
- Mode B で「誤り」「虚偽」と断定していないか
- AI が修正案・採点・推奨判断を出していないか
- Meaning Trace の各 Stage が空欄になっていないか
- 監査者の外部知識に依存した判定が、Evidence Boundary に記録されているか

## 記録形式

`examples/<case>/review/` に、以下の形式で保存します。

```markdown
# Human Review Record

- Report: <audit/ 内のファイル名>
- Reviewer: <名前>
- Date: <YYYY-MM-DD>

## Decisions

| Finding | Decision | 理由 | 次の行動 |
|---|---|---|---|
| F-01 | | | |

## Source Verification Results

| SV | 結果 | 備考 |
|---|---|---|
| SV-1 | | |

## 監査全体についての所見

## Workflow / Prompt へのフィードバック

- failure-patterns に記録した項目:
- post-freeze-candidates に記録した項目:
```
