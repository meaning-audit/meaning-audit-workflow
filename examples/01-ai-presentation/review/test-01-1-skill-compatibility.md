# Test 01-1: Skill Compatibility Check

- 目的: `skills/meaning-audit` が、既存の Prompt（`prompts/artifact-only-audit.md`）と大きく異なる監査結果を出さないかを確認する。Workflow 互換性の確認であり、どちらかの Finding を正解として扱うものではない
- Date: 2026-10-06
- 対象: Test 01-1 と同じ監査対象（Presentation Artifact — Generation Provenance Unknown）、同じ入力形式（ページ画像 36 枚 ＋ テキスト層）
- 比較元: Run 01B（既存 Prompt）→ [../audit/test-01-1-public.md](../audit/test-01-1-public.md)
- 比較先: Skill Run（`skill: meaning-audit`）。Report の原本は実名・原値を含むため Private Evidence Vault に保管し、公開しない
- 匿名化: 公開版 Report と同じ方針（固有名詞は匿名化、原値は一般化）
- Status: AI による比較。Human Review 実施済み（SC-1〜SC-4、下の 6）。追加の Run と実環境での確認は [skill-runtime-validation.md](skill-runtime-validation.md)

## 実行条件

| 項目 | Run 01B（既存 Prompt） | Skill Run |
|---|---|---|
| 監査者 | Claude Opus 5.5（文脈を持たない subagent） | Claude Opus 5.5（文脈を持たない別の subagent） |
| 指示 | `prompts/artifact-only-audit.md` の本文（Mode B 指定） | `SKILL.md` と `references/` のみを読ませ、ユーザーの依頼として「この資料を Meaning Audit してください。元資料はありません。」とだけ伝えた（Mode は指定していない） |
| 参照制限 | プロンプト、画像、テキスト層のみ。Web 検索なし | SKILL.md、references/、画像、テキスト層のみ。Web 検索なし |
| Audit Purpose | 空欄（既定値） | 指定なし（既定値） |

## 1. 構造の互換性

| 確認項目 | Run 01B | Skill Run | 一致 |
|---|---|---|---|
| 13 セクションが順序どおり | あり | あり | YES |
| Audit Mode | Mode B | Mode B（Mode を指定しなくても、Source が無いことから自動で判定） | YES |
| Mode B の定型文 | あり | あり | YES |
| Document Class | A（主）/ C（副） | C（主）/ A（副） | NO（主副が逆） |
| Audit Purpose の既定値と明記 | あり | あり | YES |
| Status の種類 | Mode B のみ | Mode B のみ | YES |
| Meaning Trace の 7 Stage | すべて記入 | すべて記入 | YES |
| Human Decision 欄 | 空欄 | 空欄（記入の選択肢だけを表示） | YES |
| 誤りの断定・修正案・点数 | なし | なし（「誤り」の語は「誤りの断定ではない」という注記にだけ現れる） | YES |
| 外部知識 | 検算のみ使用と明記 | 「なし」と明記。写真の読み取りは INFERRED | ほぼ一致 |

## 2. 件数

| 項目 | Run 01B | Skill Run |
|---|---|---|
| Meaning Unit | 32 | 38 |
| Finding | 26 | 30 |
| Key Meaning Shift | 7 | 7 |
| TRACEABLE | 0 | 1 |
| PARTIALLY TRACEABLE | 14 | 18 |
| UNTRACEABLE | 12 | 9 |
| UNKNOWN | 0 | 2 |

## 3. Finding の対応（Run 01B を基準）

Skill Run の Finding は `S-` を付けて表す（例: S-06 は Skill Run の F-06）。

| Run 01B | 内容（要約） | Skill Run | 対応 | 主な差 |
|---|---|---|---|---|
| F-01 | p6 円建て数値と表示倍率の不一致 | S-06 | 一致 | Type: VISUAL_CLAIM → OTHER。Status: PARTIALLY → UNTRACEABLE |
| F-02 | 生成AI市場から研修事業への Warrant 欠落 | S-05 | 一致 | Status: UNTRACEABLE → PARTIALLY |
| F-03 | p7 出典・シナリオ・見出しの年 | S-08 | 一部 | Skill は見出しの年と内容の年のずれに絞った（FRAMING）。出典の係り方は扱っていない |
| F-04 | p8 見出しとグラフのずれ | S-09 | 一致 | なし |
| F-05 | p9「手遅れ」 | S-10 | 一致 | Type: NARRATIVE → FRAMING |
| F-06 | p5「最も重要な理想的条件」 | S-04 | 一致 | Type: AMPLIFICATION → COMMITMENT_ESCALATION。Status: UNTRACEABLE → PARTIALLY |
| F-07 | p10 象限図の配置 | S-11 | 一致 | Status: UNTRACEABLE → PARTIALLY |
| F-08 | 「すべて解決」 | S-01 | 一致 | Skill は複数ページの絶対表現をまとめた |
| F-09 | 「開発リスクはゼロ」等 | S-02 | 一致 | Type: COMMITMENT_ESCALATION → AMPLIFICATION |
| F-10 | シミュレーションの前提 | S-14 | 一致 | Type: INFERENCE_GAP → COMPRESSION |
| F-11 | 利益額の強調 | S-15 | 一致 | Type: FRAMING → VISUAL_CLAIM。Status: PARTIALLY → TRACEABLE |
| F-12 | p29 コスト比較 | S-22, S-23 | 一致 | Skill は「目盛りの無い比較」と「費用範囲の差」の 2 件に分けた |
| F-13 | p22 事例の根拠欠落 | S-16 | 一部 | Skill は 3 事例をまとめて扱った（S-16） |
| F-14 | p23 成約率の母数 | S-18 | 一部 | Skill は成果を単一の行為に帰す強調（AMPLIFICATION）として扱い、母数の性質の推測はしていない |
| F-15 | p24 施策と成果の帰属 | S-19 | 一致 | なし |
| F-16 | 事例の「実績」表示と引用 | S-16 | 一致 | Type: QUOTE_HANDLING → INFERENCE_GAP |
| F-17 | 「受講者の声」→「導入企業の声」 | S-20 | 一致 | なし |
| F-18 | 導入企業の数値指標 | S-21 | 一致 | Type: EVIDENCE_INTERPRETATION_BLUR → CAUSAL_IMPLICATION |
| F-19 | 「陳腐化のリスクはない」 | S-25 | 一致 | Status: UNTRACEABLE → PARTIALLY |
| F-20 | 助成金と不正受給リスク | S-26 | 一致 | なし |
| F-21 | 「最高品質」と監修者 | S-13 | 一致 | なし |
| F-22 | 「職種別・業務別」 | S-27 | 一致 | なし |
| F-23 | 提供数の表記の不一致 | S-03 | 一致 | なし（どちらも OTHER） |
| F-24 | グループとの関係・設立時期・社名表記 | S-28, S-30 | 一部 | Skill はグループとの関係（S-28）と時期（S-30）を分けた。社名表記の違いは Finding にしていない |
| F-25 | 「確実に伸びる市場」 | S-29 | 一致 | Status: UNTRACEABLE → PARTIALLY |
| F-26 | 雛形の種類の不一致 | なし | 不一致 | Skill Run では検出されていない |

集計: 一致 21 件、一部一致 4 件、不一致 1 件（Run 01B の 26 件中）。

Skill Run だけにある Finding（4 件）:

| Skill Run | 内容（要約） |
|---|---|
| S-07 | p7 棒グラフの高さが表示値と合わないように見える（目視による推定。UNKNOWN / INFERRED） |
| S-12 | 「専門知識は不要」という前提と、提供形態（集合研修・伴走支援）の関係が示されていない |
| S-17 | 事例の見出し「未経験から」と、Before 欄の経歴の記述が合わない |
| S-24 | 技術サポートの範囲・方法の記述がページによって異なる |

## 4. Key Meaning Shifts の対応

| Run 01B | Skill Run | 対応 |
|---|---|---|
| KS-1 市場規模の表示倍率 | KS-1 | 一致 |
| KS-2 見出しとグラフ | KS-2 | 一致 |
| KS-3 環境データから「最も理想的」へ | KS-3 | 一致 |
| KS-4 シミュレーションとコスト比較 | KS-4 | 一致 |
| KS-5 事例の「実績」 | KS-5 | 一致 |
| KS-6 絶対的な表現 | （KS なし。Finding S-01, S-02, S-25 はある） | KS としては不一致 |
| KS-7 信頼性を支える記述の内部整合 | （KS なし。Finding S-03, S-28, S-30 はある） | KS としては不一致 |
| （なし） | KS-6 導入企業の声の指標と免責注記の有無 | Skill のみ |
| （なし） | KS-7 「専門知識不要」の前提と提供形態・サポートの記述 | Skill のみ |

## 5. 所見

- 互換性: 大きな差は見られなかった。13 セクションの構造、Mode B の判定と定型文、禁止事項の遵守、Human Decision の空欄はすべて一致した。Skill は Mode を指定しなくても Source が無いことから Mode B を選んだ
- Finding の重なり: Run 01B の 26 件中 25 件に、Skill Run の対応する Finding（一致または一部一致）がある。KS は 7 件中 5 件が一致した
- 差の性質: 差の多くは、Finding Type の選び方、Status（PARTIALLY TRACEABLE と UNTRACEABLE の境界）、Finding のまとめ方・分け方である。これらは Test 01-1 で記録済みの FP-002〜FP-004、FP-006、R-6 の観察（1 Finding に複数の所見）と同じ論点で、Skill 固有の差というより、同じ Workflow を別の実行で使ったときのばらつきと読める。ただし、同じ Prompt を 2 回実行した比較はしていないため、Skill 由来の差と実行ごとのばらつきは区別できていない
- Document Class の主副の逆転: Skill Run は `references/workflow.md` の付録 A の例（「提案スライド → C（主）/ A（副）」）に従った。この例は Workflow v1.0 の本文と同じであり、Skill による追加ではない。Class は手順を変えないため、Finding への影響は重点の置き方に限られる
- Skill の実行上の問題: `references/` の中に、Skill を単体でインストールすると読めないリポジトリ内のファイル（`docs/terminology.md`、`prompts/`、`tests/`、`examples/`）への言及が残っている。監査の実行には影響しなかったが、「OTHER が繰り返し現れたら tests/ に記録する」といった指示は、Skill の利用者には実行できない

## 6. Human Review が必要な点

| # | 確認すべき問い | Human Decision |
|---|---|---|
| SC-1 | この程度の差（Type・Status・粒度のばらつき、KS 7 件中 5 件一致）を「Workflow 互換」とみなしてよいか | ACCEPT。Workflow compatible として扱う。output equivalent とは表現しない |
| SC-2 | 同じ Prompt の 2 回目の実行と比べて、Skill 由来の差と実行ごとのばらつきを区別する必要があるか | ACCEPT。同じ条件で Skill を追加 2 回実行する（S2, S3） |
| SC-3 | Skill Run だけにある 4 件、Run 01B だけにある F-26 を、Test 01-1 の記録にどう扱うか（どちらも正解としては扱っていない） | HOLD。Workflow 変更の材料にせず、Run Variance / Compatibility Delta として記録する |
| SC-4 | `references/` に残るリポジトリ内ファイルへの言及を、Skill 用にどう扱うか（Workflow 本体は変更しない前提） | REVISE。`skills/meaning-audit/` 配下だけを Packaging Revision として修正する |
