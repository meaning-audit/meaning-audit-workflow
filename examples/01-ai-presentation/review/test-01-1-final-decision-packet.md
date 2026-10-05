# Test 01-1 Final Human Decision Packet

- Test: Test 01-1: Presentation Artifact — Generation Provenance Unknown
- Status: **FROZEN — FIELD EVIDENCE**（2026-10-06、下の 12 件の Human Decision を記入済み）
- Date: 2026-10-06
- 対象: R-3〜R-9（12 件の判断）
- 作成: Claude Opus 5.5。Evidence は既存の記録（公開版 Report、Human Review 記録、主セッションによるページ画像の直接確認）からの抜粋のみ。AI Recommendation は既存のものを維持しており、この Packet のために新しい推論は加えていない
- 判断済み（この Packet の対象外）: F-05 → REVISE（反映済み）、F-23 → REVISE（反映済み）、GitHub Support への削除依頼 → NO ACTION FOR NOW（Private の記録）

12 件の Human Decision がすべて記入されたため、Test 01-1 を `FROZEN — FIELD EVIDENCE` に変更しました。Freeze は「このテストで起きたことを記録として固定する」という意味で、Workflow の正しさを認定するものではありません。

選べる Human Decision: `ACCEPT` / `REVISE` / `HOLD` / `INVESTIGATE` / `NO ACTION`

| # | 対象 | AI Recommendation | Human Decision |
|---|---|---|---|
| 1 | R-3 / F-01 | ACCEPT | **ACCEPT** |
| 2 | R-4 / F-04 | ACCEPT | **ACCEPT** |
| 3 | R-5 / F-07 | ACCEPT | **ACCEPT** |
| 4 | R-5 / F-12 | REVISE | **REVISE** |
| 5 | R-6 / F-14 | HOLD | **REVISE** |
| 6 | R-6 / F-20 | REVISE | **REVISE** |
| 7 | R-6 / F-22 | REVISE | **REVISE** |
| 8 | R-6 / F-24 | HOLD | **HOLD** |
| 9 | R-7 / F-03 | INVESTIGATE | **NO ACTION** |
| 10 | R-7 / F-18 | HOLD | **HOLD** |
| 11 | R-8 / Run 01A | NO ACTION | **NO ACTION** |
| 12 | R-9 / Finding Granularity | HOLD | **HOLD** |

---

### 1. R-3 / F-01

**Finding**
p6 右側の円建て数値に出典・換算方法の記載が無い。円建て数値から計算される倍率（約 15 倍）は、直下の表示「20倍」と一致しない。ドル建てグラフから計算される倍率（約 20 倍）とは近い。

**Artifact Evidence**
p6 左: ドル建ての積み上げ棒グラフ（3 時点）と出典表記。p6 右: 円建ての金額（2 時点、出典表記なし）と大きな文字の「20倍の成長」。主セッションが p6 の画像を直接確認した。

**Inference**
None（成果物内の数値どうしの検算のみ。FP-005 の暫定 Human Decision により External Knowledge とはみなさない）。

**Current Status**
PARTIALLY TRACEABLE / CONFLICTING

**Issue to Decide**
この Finding を現在の内容・Status のまま記録として固定してよいか。

**AI Recommendation**
ACCEPT

**Human Decision**
ACCEPT（2026-10-06）


### 2. R-4 / F-04

**Finding**
p8 の見出し（特定の年数のうちに仕事がなくなると考える人が年々増加）は、グラフ（「確信」「不安」の 2 指標の 2 時点比較）に無い語と期間を含む。増加幅の大きい「確信」ではなく「不安」だけを見出しにしている。

**Artifact Evidence**
p8 の見出しと、同じページのグラフの題・凡例・2 時点の値。主セッションが p8 の画像を直接確認した。

**Inference**
見出しが「不安を感じている」を「仕事がなくなるかもしれない」と同一視している、という読み替えの部分（INFERRED）。見出しの語がグラフに無いこと、2 時点の比較であること、増加幅の大小は確認できる。

**Current Status**
PARTIALLY TRACEABLE / KNOWN（グラフ内容）・INFERRED（読み替え）

**Issue to Decide**
Title-body のずれとしての判定を、このまま固定してよいか。

**AI Recommendation**
ACCEPT

**Human Decision**
ACCEPT（2026-10-06）


### 3. R-5 / F-07

**Finding**
p10 は 2 軸の図に円を置き、右上を「最も理想的なビジネス環境」としているが、AI 研修事業がその位置にあることを示すデータ・配置の根拠が無い。

**Artifact Evidence**
p10 の 2 軸図（「市場の成長性」×「人材供給」）、円の配置、右上のラベル。図に数値・データの表示が無い。

**Inference**
None（根拠の表示が無いことの確認）。

**Current Status**
UNTRACEABLE / UNKNOWN

**Issue to Decide**
Visual Claim としての判定を、このまま固定してよいか。

**AI Recommendation**
ACCEPT

**Human Decision**
ACCEPT（2026-10-06）


### 4. R-5 / F-12

**Finding**
p29 の比較対象「自社で構築した場合」に金額・目盛りが無い。Service A 側は月額固定費のみで、p18-20 の表にあるアカウント利用料が含まれていない。「同等の価値」の定義も示されていない。

**Artifact Evidence**
p29: 比較対象の積み上げ棒に金額・目盛りが無い（主セッションが画像を直接確認）。Service A 側の棒は月額固定費だけ。p18-20: 表にアカウント利用料の行がある。

**Inference**
None（金額・目盛りが無いこと、費用項目が含まれないことは確認できる）。

**Current Status**
PARTIALLY TRACEABLE / CONFLICTING（p18-20 の費用構成との比較）

**Issue to Decide**
情報状態 `CONFLICTING` が妥当か。CONFLICTING の定義は「資料同士、または資料と成果物が食い違う」。p29 は p18-20 と異なる値を述べているのではなく、アカウント利用料を示していない（不提示）。不提示として扱うなら、情報状態は KNOWN になる。

**AI Recommendation**
REVISE（Finding の内容は維持し、情報状態を見直す）

**Human Decision**
REVISE（2026-10-06）


### 5. R-6 / F-14

**Finding**
p23 の成約率の分母（小さな社数）は、「興味を持つ顧客にだけ案内する」という施策の記述と並び、事前に絞られた母数である可能性がある。単価・期間・当事者は示されていない。

**Artifact Evidence**
p23 に分数で示された成約率がある。施策欄に「興味を持つ顧客にだけ案内する」趣旨の記述がある。単価・期間・当事者の記載が無い。

**Inference**
分母の社が事前に絞り込まれた母数である、という読み（INFERRED）。資料は分母の社がどう選ばれたかを述べていない。

**Current Status**
UNTRACEABLE / INFERRED（母数の性質）・UNKNOWN（その他）

**Issue to Decide**
推測を含む部分を Finding の主な内容のままにしてよいか（Status は推測に依存しない）。Finding Type（SELECTION / INFERENCE_GAP）の扱い。

**AI Recommendation**
HOLD

**Human Decision**
REVISE（2026-10-06）


### 6. R-6 / F-20

**Finding**
助成金非対応という制約を、助成金の利用と「不正受給のリスク」を結びつけることで利点として提示している。「即決しやすく利益に直結」の因果の根拠は示されていない。

**Artifact Evidence**
p31 の FAQ に、助成金非対応の説明として「審査の手間や不正受給のリスクを避け」という趣旨の記述がある。「即決しやすく利益に直結」の根拠は書かれていない。

**Inference**
「不正受給のリスク」への言及が、助成金を使う選択肢を不利に見せるという表現の効果についての解釈（Framing の判定。INFERRED）。

**Current Status**
UNTRACEABLE / INFERRED

**Issue to Decide**
1 つの Finding に入っている 2 つの所見、(a) Framing の解釈（INFERRED）と (b) 因果の根拠の欠落（確認できる）を分けるか、(b) に絞るか。

**AI Recommendation**
REVISE

**Human Decision**
REVISE（2026-10-06）


### 7. R-6 / F-22

**Finding**
p14 のレッスン名はツール・機能別が中心で、p1 のカテゴリも同様。「職種別・業務別」の構成は成果物の中では確認できない（p14 に業務別の講座が 1 件ある）。「高単価で提案できる」の根拠も無い。

**Artifact Evidence**
p14 の 1 講座分のレッスン名、p1 の画面に見えるカテゴリ、p32 の「職種別・業務別」の記述、「高単価」の根拠が無いこと。

**Inference**
p14 の 1 講座と p1 の画面から、カリキュラム全体の構成を推し量っている部分（INFERRED）。成果物に見えているのは全体の一部だけ。

**Current Status**
PARTIALLY TRACEABLE / INFERRED

**Issue to Decide**
Status を `UNKNOWN` とすべきか。成果物に見えている範囲だけでは全体の構成を判定できないとすれば UNKNOWN。現在の PARTIALLY TRACEABLE は「一部の根拠（業務別の講座 1 件）がある」と読んだもの。

**AI Recommendation**
REVISE（Status を UNKNOWN とするか確認する）

**Human Decision**
REVISE（2026-10-06）


### 8. R-6 / F-24

**Finding**
Group B の「一員」の具体的な関係、Company A との関係が示されていない。設立年月と、事例・導入企業の声・実績数との時期の関係が示されていない。p14 の画面キャプチャ内の社名は p36 の社名と表記が異なる。

**Artifact Evidence**
p34 の「グループの一員」の記述、p36 の設立年月、p14 の画面キャプチャ内の社名表記が p36 と異なること。

**Inference**
設立年月と実績の時期の関係を取り上げること自体が、実績がこの会社のものだという前提を置いている（INFERRED）。前身事業、個人の実績、グループ会社の実績、デモ環境の表示である可能性は、成果物からは判断できない（UNKNOWN）。

**Current Status**
PARTIALLY TRACEABLE / UNKNOWN（関係・時期）・CONFLICTING（社名表記）

**Issue to Decide**
1 つの Finding に 3 つの所見、(a) Group B との関係、(b) 設立時期と実績の時期、(c) 社名表記の違いが入っており、情報状態も所見ごとに異なる。このまとめ方のまま固定するか。Skill の 3 回の実行では (a) と (b) が別の Finding になり、(c) は検出されなかった。

**AI Recommendation**
HOLD

**Human Decision**
HOLD（2026-10-06）


### 9. R-7 / F-03

**Finding**
p7 の労働人口予測グラフの出典が明示されていない（Public Source 3 の表記がどの図に係るか不明）。異なるシナリオ名が並ぶ。人材不足から AI 研修事業の需要への推論は示されていない。右パネルの見出しの年と、扱う不足数の年が異なる。

**Artifact Evidence**
p7 の左グラフ（出典表記の位置が特定できない）、右パネルの見出しと不足数、ページ下部の Public Source 3 の名称と年月の表記。

**Inference**
None（出典の係り方が不明であること、シナリオ名・年の違いは確認できる）。人材不足から研修需要への Warrant が無いことも、表示が無いことの確認。

**Current Status**
PARTIALLY TRACEABLE / UNKNOWN

**Issue to Decide**
出典の係り方を確かめるために Public Source 3 を確認するか。Public Source 3 の名称と年月は資料に表記されているが、その中身は Test 01-1 では入手・確認しておらず、入手できるかどうかも UNKNOWN。確認すれば、この Finding の UNKNOWN の一部が解消する可能性がある。

**AI Recommendation**
INVESTIGATE

**Human Decision**
NO ACTION（2026-10-06）


### 10. R-7 / F-18

**Finding**
作業時間の前後が示された 2 件は、表示された削減率と整合する。残りの 4 件（業務効率、アイデア創出量、残業時間、業務への転用比率）は定義・測定方法・期間が示されていない。p28 の数値ラベルの一つは意味を特定できない。

**Artifact Evidence**
p26-28 の数値指標 6 件と、そのうち 2 件の前後の値。残り 4 件に定義の記載が無い。

**Inference**
None（整合は成果物内の検算、定義が無いことは確認できる）。

**Current Status**
PARTIALLY TRACEABLE / KNOWN（検算）・UNKNOWN（測定方法）

**Issue to Decide**
定義・測定方法を確かめるには Client A〜C の測定記録が必要で、成果物にはその入手手段が示されていない。現状のまま保留するか。

**AI Recommendation**
HOLD

**Human Decision**
HOLD（2026-10-06）


### 11. R-8 / Run 01A

**Finding**
（Finding ではなく実行の判断）Test 01-1 で Run 01A（Source-Grounded Audit）を実行するか。

**Artifact Evidence**
資料全体の Source は提供されていない。資料内で言及されている Public Source 1〜3 は名称・表記だけで、中身は入力されていない。

**Inference**
None

**Current Status**
未実行

**Issue to Decide**
Test 01-1 を Mode B（Artifact-Only）単独の記録として固定するか。Mode A と Mode B の比較は、Source と生成過程が分かっている Test 01-2 で行う方針として設計済み（`examples/01-ai-presentation/README.md` の Test 01-2 の準備）。

**AI Recommendation**
NO ACTION

**Human Decision**
NO ACTION（2026-10-06）


### 12. R-9 / Finding Granularity

**Finding**
（Finding ではなく Report の粒度の判断）Run 01B は Finding 26 件、Human Review Required 17 項目。

**Artifact Evidence**
FP-006 に記録済み。R-6 の 4 件はすべて 1 つの Finding に複数の所見を含む。Skill の 3 回の実行では Finding 28〜31 件で、まとめ方・分け方に差が出た（[skill-runtime-validation.md](skill-runtime-validation.md)）。

**Inference**
None

**Current Status**
FP-006 として保持（採用・却下はしていない）

**Issue to Decide**
粒度の問題を、Workflow を変えずに Field Evidence として保持するか。現時点では Workflow v1.0 の変更は行わない。

**AI Recommendation**
HOLD

**Human Decision**
HOLD（2026-10-06）

