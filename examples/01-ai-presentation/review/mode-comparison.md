# Test 01-1: Mode Comparison Review（公開版）

- Test: Test 01-1: Presentation Artifact — Generation Provenance Unknown
- Status: AI による比較の準備（Human Review の判断は [test-01-1-human-review.md](test-01-1-human-review.md)）
- Date: 2026-10-06
- 作成: Claude Opus 5.5（テストを実行した主セッション。Run 01B の監査者とは別のコンテキスト）
- 対象 Report: [../audit/test-01-1-public.md](../audit/test-01-1-public.md)
- 匿名化: 固有名詞は公開版 Report の対応表に従う

---

## 0. 実行状況

| Run | Mode | 状態 | 理由 |
|---|---|---|---|
| Run 01A | Source-Grounded | 未実行 | Source（元資料）が提供されていない。資料内で言及されている外部資料（Public Source 1〜3）は名称・URL だけで、中身は入力されていない |
| Run 01B | Artifact-Only | 実行済み | `prompts/artifact-only-audit.md` を無改変で使用。この会話の文脈を持たない別の subagent に、プロンプト・ページ画像・テキスト層だけを渡して実行した |

Run 01A が無いため、Mode A と Mode B の比較（下の項目 1〜3、6、7）は今回はできない。

独立性: Run 01B の監査者は、Workflow の文書、他の Report、Web 検索のいずれも参照していない（実行時にそう指示した）。

## 0.1 主セッションによる読み取りの照合

主セッションが 5 ページ（p6, p8, p14, p29, p36）の画像を直接確認し、Report の読み取りと照合した。

| ページ | Report の記述 | 照合結果 |
|---|---|---|
| p6 | ドル建てグラフの値、右側の円建て数値に出典表記が無いこと、表示倍率「20倍」 | 一致 |
| p8 | グラフは「確信」「不安」の 2 時点比較（増加幅は「確信」の方が大きい）。見出しは将来の失業不安が年々増加という趣旨 | 一致 |
| p14 | 画面キャプチャ内の社名表記が会社概要と異なる。表の動画本数の合計 | 一致（合計を再計算） |
| p29 | 比較対象の棒に金額・目盛りが無い。Service A 側は月額固定費のみ | 一致 |
| p36 | 会社概要の設立年月 | 一致 |

これは Report が資料を正しく読んでいるかの確認で、資料の内容が正しいかの確認ではない。

---

## 1. 両モードで共通して検出された Finding

比較できない（Run 01A 未実行）。

## 2. Source-Grounded Audit でのみ検出された Finding

比較できない。Run 01A を実行すれば、次が判定対象になると見込まれる。

- p6 の円建て数値と表示倍率「20倍」が、Public Source 1 のどの数値に対応するか（F-01）
- p8 の見出しに当たる設問が Public Source 2 にあるか（F-04）
- p7 の労働人口グラフと人材不足の数値が、Public Source 3 と合っているか（F-03）

## 3. Artifact-Only Audit でのみ検出された Finding

比較できない。Run 01B の Finding の多くは成果物の中の不整合や Warrant の欠落で、Source の有無に左右されない可能性がある。Run 01A でも同じものが出るかは、次回の観察対象とする。

## 4. Artifact-Only でも十分追跡できた Meaning Shift

| KS | 内容 | 追跡できた理由 |
|---|---|---|
| KS-1 | p6 の表示倍率と円建て数値の不一致 | グラフと右側の数値を成果物の中で検算できた |
| KS-2 | p8 の見出しとグラフの内容のずれ | 見出しとグラフ題・凡例が同じページにある |
| KS-4 | シミュレーションの前提が書かれていない点、p29 の費用範囲の差 | 表の数値から合計と単価を逆算できた |
| KS-5 | p24 の施策（営業スクリプトの変更）と成果指標の帰属のずれ | 見出し・施策欄・数値ラベルが同じページにある |
| KS-7 | 提供本数の表記、社名表記、設立時期と実績の関係 | ページをまたいで成果物の中で照合できた |

## 5. Source が無いことで UNKNOWN / UNTRACEABLE になった箇所

- **UNTRACEABLE（12 件）：** F-02, F-05, F-06, F-07, F-09, F-13, F-14, F-16, F-19, F-20, F-21, F-25。多くは「推論の根拠が成果物に無い」もので、Source があっても解消しない可能性がある
- **Source があれば解消しうる Unknown：** Critical Unknowns 1, 3, 7
- **統計資料ではなく料金表・契約書・社内記録が要る Unknown：** Critical Unknowns 2, 4, 5, 8。Class C 的な文書では、「元資料」の範囲が広がる

## 6. Source 確認によって判定が変わった箇所

比較できない（Run 01A 未実行）。

## 7. Mode B で過剰に推定した可能性のある Finding

F-14, F-20, F-22, F-24。整理は [test-01-1-human-review.md](test-01-1-human-review.md) の 4。

補足: F-01 の CONFLICTING の対象は円建て数値の側で、「20倍」はグラフの比率とは合う。Finding Ledger はこの区別を保っているが、Key Meaning Shifts の要約では区別が弱い。

禁止事項（Mode B での誤りの断定、修正案、点数）への違反は見当たらなかった。

## 8. Mode B の実務上の有用性

- 有用だった点: 外部資料が無くても、「見出しの強さ」「検算できる不一致」「前提の欠落」「因果の帰属」は具体的に指摘できた。Source Verification Required（14 件）は、確認作業のチェックリストとして使える
- 限界: 外部統計の引用が正しいか、事例・お客様の声が実在するか、それらの数値が正しいかは言えない。影響の大きい主張ほど UNTRACEABLE か UNKNOWN になる
- 量: Finding 26 件、Human Review Required 17 件は、レビュー担当者の負担としては多い

## 9. Workflow の不足（観察。修正はしない）

FP-001〜FP-004、FP-006（[../../../tests/failure-patterns.md](../../../tests/failure-patterns.md)）。加えて、Class C 的な資料では「元資料」の範囲（統計か、契約書・社内記録か）によって Mode A の意味が変わる。

## 10. Prompt の不足（観察。修正はしない）

- Overall Finding の「3〜6 文」は、Finding が多いと窮屈になる
- Finding Ledger の Stage 列に、定義に無い値（範囲の表記）が使われた
- INPUT 欄に、作成者・作成日・生成ツールを書く場所が無い
- Finding 数・Human Review 項目数の目安が無い

## 11. 新しい概念の候補

PFC-003、PFC-004（[../../../tests/post-freeze-candidates.md](../../../tests/post-freeze-candidates.md)）。Workflow には追加していない。
