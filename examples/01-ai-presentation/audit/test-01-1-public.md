# Test 01-1 Public Audit Record

- Test: Test 01-1: Presentation Artifact — Generation Provenance Unknown
- Workflow version: Meaning Audit Workflow v1.0
- Prompt: `prompts/artifact-only-audit.md`（無改変）
- Auditor: Claude Opus 5.5（Claude Code の subagent。テスト実行セッションの文脈を持たない状態で実行）
- Date: 2026-10-06
- Review status: FROZEN — FIELD EVIDENCE（Human Review 済み。[../review/test-01-1-human-review.md](../review/test-01-1-human-review.md)）

## この記録について

これは Meaning Audit Workflow v1.0 のフィールドテストの記録であり、特定の企業・サービスを公に評価するものではありません。

> Public 版では第三者の再特定リスクを下げるため、企業名・個人名・商品名・一部の固有値を匿名化または一般化している。原値および非匿名化記録は Private Evidence として保存している。Meaning Audit 上の Finding の意味は維持している。

- AI が出力した Report の原本（実名・原値入り）は、公開しない Private Evidence Vault に保管しています
- 維持しているもの: ページ番号、Finding ID、Meaning Unit ID、Finding Type、Status、情報状態、Finding が成立するための数値の関係（一致・不一致、倍率の大小、増加幅の大小など）
- 一般化したもの: 金額、割合、件数、本数などの原値（概数・桁・関係に置き換え）、資料の特徴的な言い回し（趣旨に言い換え）
- 各 Finding は「成果物の中で根拠がどう示されているか」についての所見であり、記載内容が事実と異なるという判定ではありません
- 公開版と原本の意味の一致は、[../review/test-01-1-human-review.md](../review/test-01-1-human-review.md) の 6 で照合しています

### 匿名化の対応

| 表記 | 指すもの |
|---|---|
| Company A | 監査対象資料の発行元企業 |
| Service A | 資料で紹介されているサービス（AI 研修教材と学習管理システムを、他社が自社ブランドで再販できるようにするもの） |
| Group B | Company A / Service A が所属すると記載されている上場企業グループ |
| Client A / B / C | 資料の「導入企業の声」に掲載された企業 |
| Representative A / B / C | Client A / B / C の代表者 |
| Public Source 1 | 生成AI市場の需要額見通し（グラフの出典として表記あり） |
| Public Source 2 | 働く人の AI 意識についての調査（出典表記あり） |
| Public Source 3 | IT 人材の需給についての調査（出典表記あり） |

---

## Human Review 後の Finding 修正

この公開版は、AI が出力した Report（原本）に、Human Decision による修正を反映したものです。修正したのは下の 4 件だけで、Finding 番号は変えていません。

| Finding | Human Decision | 修正内容 |
|---|---|---|
| F-12 | REVISE | 情報状態を CONFLICTING から KNOWN に変更。成果物から確認できるのは、比較の金額・目盛り・費用項目・定義が示されていないこと（不提示）であり、成果物内で相反する記述があるわけではないため |
| F-14 | REVISE | 母数についての推測を外し、「分数形式の成約実績があるが、母集団の定義・期間・選定条件は確認できない」という範囲に限定した。情報状態を UNKNOWN に変更 |
| F-20 | REVISE | Observation（因果の根拠の不提示、KNOWN）と Interpretation（Framing の解釈、INFERRED）を分けて記載 |
| F-22 | REVISE | 見えている範囲からは全体の構成を判断できないため、Status を PARTIALLY TRACEABLE から UNKNOWN に変更 |
| F-24 | HOLD | 内容は変えず、「3 つの所見を含む」という Human Review 注記を加えた |

## 1. Audit Object

| 項目 | 内容 |
|---|---|
| 名称 | Service A のサービス紹介資料（匿名化） |
| 形式 | PDF、36 ページ、16:9 スライド。ページ画像 36 枚と PDF テキスト層を入力（テキスト層があるのは一部のページのみ） |
| 作成者 / 生成元 | 資料上の表記は Company A。実際の作成者・生成手段（AI 生成か否かを含む）は UNKNOWN |
| 作成日 | UNKNOWN（フッターの年表記と、会社概要の設立年月の記載あり） |
| 監査範囲 | 全 36 ページ（表紙・中扉を含む） |

## 2. Audit Mode

- Mode: Mode B: Artifact-Only Audit
- 判定理由: 元資料（Source）が提供されておらず、入力は成果物のみであるため
- Source verification は実施できない。外部 Evidence がないため、本 Report は成果物内部の Traceability のみを判定し、誤りの断定は行わない。

## 3. Document Class

- Class: 主 Class A: Presentation / Visualization ／ 副 Class C: Proposal / Analysis / Decision Document
- 判定理由: スライド形式で、市場グラフ・象限図・コスト比較の棒グラフ・大きな数値表示など視覚表現が主な伝達手段（Class A）。同時に、読み手（研修事業を始める事業者候補）に Service A の導入判断を促す営業提案資料（Class C）
- 重点観点: Class A の 7 観点 ＋ Class C の Evidence, Inference, Warrant, Recommendation, Commitment

## 4. Audit Purpose

- 目的: Meaning Shift の所在を明らかにする（AUDIT_PURPOSE が空欄のため既定値を使用）

## 5. Evidence Boundary

| 区分 | 内容 |
|---|---|
| 参照した Source | なし（成果物のみ） |
| 成果物内で言及されているが提供されていない Source | (1) p6 グラフの出典 Public Source 1 (2) p7 Public Source 3 (3) p8 Public Source 2 (4) p6 右側の円建て金額の出典（記載なし） (5) p7 労働人口予測グラフの出典（明示なし） (6) p18-20 シミュレーションの前提データ (7) p22-24 事例の元データ・当事者 (8) p26-28 Client A〜C の測定データ・発言記録 (9) p16 監修者の経歴の根拠 (10) p34 Group B の会社情報 (11) p36 Company A の会社情報 |
| 監査対象の範囲 | 全 36 ページ。ページ画像を読み取り、テキスト層と照合 |
| 監査者が持ち込んだ外部知識 | 真偽の判定には使っていない。使ったのは日本語の読解、成果物内の数値どうしの検算、営業資料の一般的な構造についての知識のみ。外部知識から照合が必要と考えた点は、真偽を書かずに Section 11 に挙げた |

## 6. Overall Finding

資料は「悩み → すべて解決 → 市場・人材・意識の環境 → 手遅れになる → サービス詳細 → 収益シミュレーション → 事例・声 → コスト比較 → FAQ → 会社情報」という流れで、外部統計からサービス導入の判断までを一続きの物語として提示している。外部統計のページ（p6-p8）には出典表記があるが、グラフの数値と表示倍率・別単位の数値の食い違い（p6）や、見出しとグラフの内容のずれ（p8）が成果物の中で見られる。生成AI市場や労働人口のデータから「AI 研修事業が最も理想的」「確実に伸びる」へ至る Warrant は示されていない。収益シミュレーション（p18-20）は計算を成果物の中で追跡できるが、前提が明示されておらず、p29 のコスト比較とは費用の範囲が一致しない。事例（p22-24）と導入企業の声（p26-28）の数値は、当事者・期間・測定方法が示されておらず、「すべて」「ゼロ」「リスクはない」といった強い Commitment が多くのページで使われている。

## 7. Key Meaning Shifts

| # | Meaning Unit | Shift の内容 | Stage | Finding |
|---|---|---|---|---|
| KS-1 | MU-07, MU-08（p6 市場規模） | ドル建てグラフ（計算上は約 20 倍）が、出典の無い円建て数値（計算上は約 15 倍）に置き換えられたうえで「20倍の成長」と表示される。対象は生成AI市場（世界）全体で、AI 研修事業の市場ではない | Interpretation → Context | F-01, F-02 |
| KS-2 | MU-10（p8 意識の変化） | グラフの「AI の影響を確信している／不安を感じている」が、見出しでは「特定の年数のうちに自分の仕事がなくなると考える人が年々増加」に置き換えられる | Interpretation → Context（Title-body） | F-04 |
| KS-3 | MU-06, MU-11, MU-12, MU-31（p5, p9, p10, p35） | 市場拡大・人材不足・意識の変化という外部状況が、Warrant の提示なしに「最も理想的な条件」「乗らないと手遅れ」「確実に伸びる市場」へと段階的に強められる | Inference → Commitment | F-03, F-05, F-06, F-07 |
| KS-4 | MU-18〜MU-20, MU-25（p18-20, p29） | 前提が部分的にしか示されないシミュレーションの合計値が、大きな「利益」額として提示される。p29 では月額コストが月額固定費のみで表示される（p18-20 にあるアカウント利用料が p29 には現れない） | Interpretation → Commitment | F-10, F-11, F-12 |
| KS-5 | MU-21〜MU-23（p22-24） | 当事者・期間・母数が示されない事例が「実績」として提示され、p24 では営業スクリプト変更の結果が「Service A 導入後のアポ率」として Service A に帰属される | Evidence → Inference（Causal） | F-13, F-14, F-15 |
| KS-6 | MU-03〜MU-05, MU-14, MU-26（p3, p4, p12, p15, p31） | 範囲・条件が示されない「すべて解決」「開発リスクはゼロ」「陳腐化のリスクはない」などの絶対的な表現で Commitment が提示される | Commitment | F-08, F-09, F-19 |
| KS-7 | MU-13, MU-16, MU-30, MU-32（p1, p12, p14, p34, p36） | 提供本数の表記、社名表記、設立時期と実績の時期、Group B との関係など、信頼性を支える記述が成果物の中で相互に整合づけられていない | Evidence → Context | F-17, F-18, F-23, F-24 |

## 8. Meaning Trace

### KS-1: 市場規模の表示倍率

| Stage | Trace |
|---|---|
| Evidence / Source | 外部 Source なし。成果物内の根拠: p6 左の積み上げ棒グラフ（生成AI市場の需要額見通し・世界、ドル建て、3 時点）と年平均増加率の表示、出典 Public Source 1。p6 右の円建て金額（2 時点）には出典表記なし（KNOWN） |
| Interpretation | 見出しの市場規模はグラフの最終年の値と対応する（KNOWN）。右側は単位がドルから円に変わり、換算方法の記載は無い（KNOWN）。グラフから計算される倍率は約 20 倍、円建て数値から計算される倍率は約 15 倍で、両年の円/ドル比も一致しない（KNOWN: 成果物内の検算） |
| Inference / Warrant | 表示倍率「20倍」はグラフの倍率とは近いが、直上の円建て数値の倍率とは一致しない（CONFLICTING）。円建て数値の出どころは UNKNOWN |
| Context / Pragmatics | 生成AI市場全体（基盤モデル・アプリ・ソリューションの合計、世界）が、AI 研修事業の成長性の根拠として配置されている。両者をつなぐ Warrant は示されていない（INFERRED: 配置からの読み取り） |
| Commitment / Presented Meaning | 大きな装飾文字で「20倍の成長」と断定的に提示され、p35 の「確実に伸びていく市場」につながる |
| Finding | F-01（VISUAL_CLAIM / CONFLICTING）、F-02（INFERENCE_GAP） |
| Status | PARTIALLY TRACEABLE（グラフには出典表記がある。円建て数値と表示倍率は成果物内で食い違う） |

### KS-2: 意識の変化の見出しとグラフ

| Stage | Trace |
|---|---|
| Evidence / Source | 外部 Source なし。成果物内の根拠: p8 のグラフ「AI が仕事に与える影響への意識」。「確信している」「不安を感じている」の 2 指標の 2 時点比較で、どちらも増加。増加幅は「確信」の方が大きい。出典 Public Source 2（KNOWN） |
| Interpretation | グラフが示すのは 2 指標の 2 時点比較で、見出しにある年数や「仕事がなくなる」という語はグラフに無い（KNOWN） |
| Inference / Warrant | 見出しは「不安を感じている」を「将来自分の仕事がなくなるかもしれない」と同一視し、2 時点の変化を「年々増加」と一般化している。この読み替えの根拠は示されていない（INFERRED） |
| Context / Pragmatics | 増加幅の大きい「確信」は見出しに採られず、「不安」の側だけが見出しになっている（Selection）。調査対象の国・属性はページ上で読み取れない（UNKNOWN） |
| Commitment / Presented Meaning | 「年々増加している」と断定形で提示され、p9「手遅れになる」に続く |
| Finding | F-04（TITLE_BODY_GAP）、F-05（NARRATIVE） |
| Status | PARTIALLY TRACEABLE |

### KS-3: 環境データから「最も理想的」「手遅れ」「確実に伸びる」へ

| Stage | Trace |
|---|---|
| Evidence / Source | 外部 Source なし。成果物内の根拠: p6（生成AI市場）、p7（労働人口予測、IT 人材・AI 人材の不足数、Public Source 3 の表記）、p8（Public Source 2） |
| Interpretation | p5 は 3 つの要素を「×」で結び「最も重要な理想的条件が整っている」とまとめる。p10 は「市場の成長性」×「人材供給」の 2 軸に円を置き、右上を「最も理想的なビジネス環境」とする（KNOWN） |
| Inference / Warrant | 人材不足 → AI 研修の需要、生成AI市場の拡大 → AI 研修事業の成長、不安 → 研修需要、AI 研修事業が p10 の右上に位置する、のいずれも Warrant が示されていない（INFERRED）。p10 の円の位置がデータに基づくことも示されていない（UNKNOWN） |
| Context / Pragmatics | p9 は、写真（Visual observation: こぼれた硬貨と排水口が写っている）と「今乗らないと手遅れ」という文を組み合わせ、損失回避の Framing をつくる（Interpretation）。p35 の代表者メッセージは「確実に伸びていく市場」と結ぶ |
| Commitment / Presented Meaning | 「最も重要」「最も理想的」「手遅れ」「確実に」と、根拠の範囲を超える強さで結論づけられる |
| Finding | F-03, F-05, F-06, F-07 |
| Status | UNTRACEABLE（各統計には出典表記があるが、結論への推論の道筋が示されていない） |

### KS-4: 収益シミュレーションと「利益」・コスト比較

| Stage | Trace |
|---|---|
| Evidence / Source | 外部 Source なし。成果物内の根拠: p18-20 の 12 か月の表（月額固定費、契約数、単価、売上、アカウント利用料、利益）と前提の見出し、注記「成果を保証するものではない」。p29 の棒グラフ（Service A の月額費用） |
| Interpretation | 3 つのシナリオとも、見出しの売上・原価・利益（年間で数百万〜数千万円規模）は表の合計と検算で一致する（1 つは丸めの範囲で一致）（KNOWN: 検算）。アカウント利用料の単価は表からの逆算で、本文には明記されていない（INFERRED） |
| Inference / Warrant | 表は、解約が無いこと、集客・営業費や人件費が無いこと（原価がシステム関連費用のみ）、p19 では年額が契約月に一括計上されることを前提にしている。これらの前提は文章で示されていない（INFERRED） |
| Context / Pragmatics | 3 つのシナリオとも「利益」が大きな赤字で強調される。シミュレーションの単価は p13 の価格設計の例と異なり、関係が示されていない。p29 では Service A 側のコストが月額固定費のみで、比較対象「自社で構築した場合」には金額・目盛りが無い |
| Commitment / Presented Meaning | 売上・原価・利益の額が見出し級の結論として提示される。p29 は「月額固定費で同等の価値を自社でつくるのは現実的でない」と結論づける |
| Finding | F-10, F-11, F-12 |
| Status | PARTIALLY TRACEABLE（計算は追跡できるが、前提と費用の範囲の提示に欠落がある） |

### KS-5: 事例の「実績」

| Stage | Trace |
|---|---|
| Evidence / Source | 外部 Source なし。成果物内の根拠: p22（開始から短期間での売上（数百万円規模）と高い粗利率、当事者の発言）、p23（月額の継続売上（百万円規模）と分数で示された成約率、発言）、p24（施策の前後のアポ率、発言）。いずれも当事者・業種・時期・測定期間・母数の記載なし。各ページに「成果を保証するものではない」の注記 |
| Interpretation | p24 の見出しの倍率は、前後のアポ率から計算した値と一致する（KNOWN）。p23 の成約実績は分数形式で示されているが、母集団の定義・対象期間・選定条件は示されていない（UNKNOWN） |
| Inference / Warrant | p24 の施策は営業スクリプトの変更で、見出しもそう述べるが、数値のラベルは「Service A 導入後のアポ率」として Service A に帰属させている。比較期間・件数・他の要因は示されていない（INFERRED） |
| Context / Pragmatics | 中扉で事例を「実績」と位置づけ、各ページに「実績達成」のバッジを付ける。p22 の売上が p18-20 のシミュレーションのどの条件に当たるかは示されていない。p36 の設立年月との時期の関係も示されていない |
| Commitment / Presented Meaning | 「未経験から短期間で高い売上」「一言の提案で継続売上が増加」「劇的改善」と、断定的な成果として提示される |
| Finding | F-13, F-14, F-15, F-16 |
| Status | UNTRACEABLE（数値の根拠・当事者・期間が示されていない） |

### KS-6: 絶対的な表現による Commitment

| Stage | Trace |
|---|---|
| Evidence / Source | 外部 Source なし。成果物内の根拠: p2 の悩み 5 件、p4 の解決項目 3 件、p12 の提供物リスト、p15 のツール 4 件、p31 の FAQ 回答 |
| Interpretation | p3「すべて解決」は p2 の 5 つの悩みを受けるが、それぞれの悩みとの対応は p4 の 3 項目でまとめて示されるだけ（KNOWN）。導入コスト・期間・開始までの日数についての具体的な表現（「数百万円」「半年以上」「最短○週間」「最短即日」）の根拠は示されていない（UNKNOWN） |
| Inference / Warrant | 「開発リスクはゼロ」「すべて提供」「陳腐化のリスクはない」は、提供範囲の列挙から「残るリスクは無い」への推論を含むが、範囲・条件が示されていない（INFERRED） |
| Context / Pragmatics | p31 の助成金の FAQ は、非対応の説明の中で「不正受給のリスク」に触れている（Observation）。これにより非対応という制約が利点として Framing されている（Interpretation、INFERRED） |
| Commitment / Presented Meaning | 「すべて」「ゼロ」「リスクはない」「利益に直結」と、最大の強さで提示される |
| Finding | F-08, F-09, F-19, F-20 |
| Status | UNTRACEABLE |

### KS-7: 信頼性を支える記述の内部整合

| Stage | Trace |
|---|---|
| Evidence / Source | 外部 Source なし。成果物内の根拠: p4・p12 の提供本数（「○○本以上」）、p14 の提供数（「○○種類以上」）、p1・p33 の画面キャプチャの件数表示、p14 の画面キャプチャ内の社名表記、p36 の会社概要（設立年月など）、p34 の Group B の記述、p16 の監修者の経歴 |
| Interpretation | 「本」と「種類」で単位が揺れる。p14 の表に示される 1 講座分の動画本数の合計を検算で求めた（KNOWN: 検算。原値は Private Evidence に保管）。画面キャプチャの件数表示が何の件数かは示されていない（UNKNOWN） |
| Inference / Warrant | 会社概要の設立年月と、事例・導入企業の声・監修者の実績との時期の関係（前身事業やグループ会社の実績か等）は説明されていない（UNKNOWN）。Group B との資本関係・位置づけも示されていない（UNKNOWN） |
| Context / Pragmatics | p34 ではサービス名を主語として「グループの一員」と述べ、上場企業グループへの所属を「継続性」の根拠として配置している。p34 の Group B の所在地と p36 の Company A の所在地は同じ表記だが、両者の関係は説明されていない |
| Commitment / Presented Meaning | 「最高品質のカリキュラム」（p16）、「グループの経営基盤の上で継続する」（p34）と、品質と提供継続の保証に近い形で提示される |
| Finding | F-17, F-18, F-21, F-23, F-24 |
| Status | PARTIALLY TRACEABLE |

## 9. Finding Ledger

| ID | Meaning Unit | Location | Stage | Finding Type | 内容 | Status | 情報状態 | 根拠（成果物内の箇所） |
|---|---|---|---|---|---|---|---|---|
| F-01 | MU-08 円建て市場規模と表示倍率「20倍」 | p6 右 | Interpretation | VISUAL_CLAIM | 円建て数値に出典・換算方法の記載が無い。円建て数値から計算される倍率は約 15 倍で、直下の表示「20倍」と一致しない。ドル建てグラフから計算される倍率（約 20 倍）とは近い。両年の円/ドル比も一致しない | PARTIALLY TRACEABLE | CONFLICTING | p6 左グラフと右パネルの比較 |
| F-02 | MU-07 市場の成長性 | p6, p5 | Inference / Warrant | INFERENCE_GAP | 生成AI市場（世界）全体の需要額が、AI 研修事業の成長性の根拠として使われているが、両者をつなぐ Warrant が示されていない | UNTRACEABLE | INFERRED | p6 グラフ題、p5 |
| F-03 | MU-09 労働人口の減少、IT 人材・AI 人材の不足 | p7 | Inference / Warrant | INFERENCE_GAP | 労働人口予測グラフの出典が明示されていない（Public Source 3 の表記がどの図に係るか不明）。異なるシナリオ名が並ぶ。人材不足から AI 研修事業の需要への推論は示されていない。右パネルの見出しの年と、扱う不足数の年が異なる | PARTIALLY TRACEABLE | UNKNOWN | p7 左グラフ、右パネル、出典表記 |
| F-04 | MU-10 特定の年数のうちに仕事がなくなると考える人が年々増加 | p8 | Context / Pragmatics | TITLE_BODY_GAP | グラフは「確信」「不安」の 2 時点比較で、見出しの年数や「仕事がなくなる」はグラフに無い。2 時点から「年々」と一般化。増加幅の大きい「確信」ではなく「不安」だけを見出しにしている | PARTIALLY TRACEABLE | KNOWN（グラフ内容）／INFERRED（読み替え） | p8 見出し、グラフの題・注・数値 |
| F-05 | MU-11 今乗らないと手遅れになる | p9 | Commitment | NARRATIVE | p6-p8 の統計の直後に、根拠の提示なしに損失回避の結論が置かれ、画像（Visual observation: 排水口とこぼれた硬貨の写真）で強められている。何に対して「手遅れ」なのかも示されていない | UNTRACEABLE | UNKNOWN | p9、p6-p8 からの配置 |
| F-06 | MU-06 最も重要な理想的条件が整っている | p5 | Inference / Warrant | AMPLIFICATION | 3 要素の列挙から「最も重要」「理想的」への推論の根拠が示されていない。カードには要素名だけで数値・説明が無い | UNTRACEABLE | INFERRED | p5 |
| F-07 | MU-12 AI 研修事業の市場での位置、最も理想的なビジネス環境 | p10 | Context / Pragmatics | VISUAL_CLAIM | 2 軸の図に円を置き右上を「最も理想的」とするが、AI 研修事業がその位置にあることを示すデータ・配置の根拠が無い。他の事業との比較も示されていない | UNTRACEABLE | UNKNOWN | p10 図 |
| F-08 | MU-03 すべて解決 | p3（p2→p4） | Commitment | AMPLIFICATION | p2 の 5 つの悩みと p4 の 3 項目の対応が明示されず、「すべて」の範囲が示されていない | PARTIALLY TRACEABLE | INFERRED | p2, p3, p4 |
| F-09 | MU-04 コストと期間を省き開発リスクをゼロに、短期間で販売開始 | p4（p2, p15, p32） | Commitment | COMMITMENT_ESCALATION | 導入コスト・期間・開始までの日数についての具体的な表現の根拠が示されていない。教材を開発しないことを「開発リスクはゼロ」と表現し、外部サービスに依存することのリスクには触れていない | UNTRACEABLE | UNKNOWN | p2, p4, p15, p32 |
| F-10 | MU-18〜MU-20 収益シミュレーション（3 シナリオの利益額） | p18-20 | Inference / Warrant | INFERENCE_GAP | 見出しの合計は表と整合するが、解約ゼロ・累積、集客/営業費・人件費ゼロ、アカウント利用料の単価（逆算）、p19 の年額一括計上といった前提が文章で示されていない。「原価」の範囲がシステム関連費用のみ | PARTIALLY TRACEABLE | KNOWN（表）／INFERRED（前提） | p18-20 |
| F-11 | MU-18〜MU-20 利益額の強調 | p18-20 | Context / Pragmatics | FRAMING | 「成果を保証しない」は小さな注記で、利益額は大きな赤字で提示される。シミュレーションの単価は p13 の価格設計の例と異なり、どの条件で現実的かは示されていない | PARTIALLY TRACEABLE | KNOWN | p13, p18-20 |
| F-12 | MU-25 同等の価値を生むコスト比較 | p29 | Context / Pragmatics | VISUAL_CLAIM | 比較対象「自社で構築した場合」に金額・目盛りが無く、棒の高さの根拠が示されていない。Service A 側は月額固定費のみで、p18-20 の表にあるアカウント利用料は p29 に示されていない。「同等の価値」の定義も示されていない | PARTIALLY TRACEABLE | KNOWN（金額・目盛り・費用項目・定義の不提示を成果物内で確認） | p29, p18-20 |
| F-13 | MU-21 未経験から短期間で高い売上と粗利率 | p22 | Evidence → Interpretation | EVIDENCE_INTERPRETATION_BLUR | 当事者、時期、単価・顧客数、粗利率の算定範囲が示されていない。発言中の「初月から黒字」の根拠も無い。p18-20 のシミュレーションとの関係も説明されていない | UNTRACEABLE | UNKNOWN | p21, p22 |
| F-14 | MU-22 一言の提案で継続売上が増加、分数で示された成約実績 | p23 | Inference / Warrant | SELECTION | 分数形式の成約実績が提示されているが、母集団の定義、対象期間、選定条件は資料内で確認できない。単価・当事者も示されていない。数値が虚偽とは判定しない。ただし、その数値をどこまで一般化してよいかは成果物から判断できない | UNTRACEABLE | UNKNOWN（母集団の定義・期間・選定条件） | p23 施策欄・成果欄 |
| F-15 | MU-23 営業スクリプトの変更でアポ率が数倍、Service A 導入後のアポ率 | p24 | Inference / Warrant | CAUSAL_IMPLICATION | 見出しの倍率は前後のアポ率と整合する。施策は「営業スクリプトの変更」と説明される一方、成果指標は「Service A 導入後のアポ率」として提示されている。施策と成果の帰属関係が資料内では追跡できない。比較期間・コール数・他の要因は示されていない | PARTIALLY TRACEABLE | KNOWN（比率）／INFERRED（帰属） | p24 見出し・施策欄・成果欄 |
| F-16 | MU-21〜MU-23「実績達成」表示と発言の引用 | p21-24 | Context / Pragmatics | QUOTE_HANDLING | 引用された発言に発言者名・属性・時期が無く、成果物の中では当事者を特定できない。中扉で「実績」と位置づけ、各事例にバッジを付けている | UNTRACEABLE | UNKNOWN | p21-24 |
| F-17 | MU-24「受講者の声」→「導入企業の声」 | p25-28 | Context / Pragmatics | TITLE_BODY_GAP | 中扉は「受講者の声」だが、各ページは「導入企業の声」で発言者は代表者（Representative A〜C）。導入企業が再販事業者経由の受講企業か、Service A の直接顧客かも示されていない | PARTIALLY TRACEABLE | KNOWN | p25, p26-28 |
| F-18 | MU-24 導入企業の数値指標（割合・倍率・時間の 6 件） | p26-28 | Evidence → Interpretation | EVIDENCE_INTERPRETATION_BLUR | 作業時間の前後が示された 2 件は、表示された削減率と整合する。残りの 4 件（業務効率、アイデア創出量、残業時間、業務への転用比率）は定義・測定方法・期間が示されていない。p28 の数値ラベルの一つは意味を特定できない | PARTIALLY TRACEABLE | KNOWN（検算）／UNKNOWN（測定方法） | p26-28 |
| F-19 | MU-26 自動で最新化されるため陳腐化のリスクはない | p31（p4） | Commitment | COMMITMENT_ESCALATION | 更新の頻度・範囲・契約上の条件が示されないまま、リスクが無いと断定される | UNTRACEABLE | UNKNOWN | p4, p31 |
| F-20 | MU-27 助成金非対応、不正受給のリスクを避け、即決しやすく利益に直結 | p31 | Inference / Warrant | FRAMING | Observation: 「即決しやすく利益に直結」という因果を支える根拠が、成果物内に提示されていない。Interpretation（INFERRED）: 助成金非対応の説明で「不正受給のリスク」に触れることにより、非対応という制約が利点として提示されている、という Framing の解釈 | UNTRACEABLE | KNOWN（Observation: 根拠の不提示）／INFERRED（Interpretation: Framing） | p31 |
| F-21 | MU-17 最高品質のカリキュラム、監修者の経歴 | p16 | Commitment | AMPLIFICATION | 「最高品質」の比較基準が示されていない。「監修」の具体的な役割、経歴中の数値の根拠も示されていない | UNTRACEABLE | UNKNOWN | p16 |
| F-22 | MU-28 職種別・業務別に特化した実践的カリキュラムで差別化 | p32（p14, p1） | Inference / Warrant | INFERENCE_GAP | 成果物に見えている範囲（p14 の 1 講座分のレッスン名、p1 の画面のカテゴリ）は、ツール・機能別のものが中心で、業務別の講座が 1 件ある。カリキュラム全体が「職種別・業務別」に構成されているかは、見えている範囲からは判断できない。「高単価で提案できる」の根拠は示されていない | UNKNOWN | KNOWN（見えている範囲の構成、高単価の根拠の不提示）／UNKNOWN（全体の構成） | p1, p14, p32 |
| F-23 | MU-13 提供本数「○○本以上」「○○種類以上」 | p4, p12, p14（p1, p33） | Evidence → Interpretation | OTHER（数量表記の不一致） | 単位が「本」と「種類」で揺れる。p14 の表（1 講座分の動画本数の合計）と画面キャプチャの件数表示が、表示された提供数とどう関係するか示されていない。p14 の表の時間の列は見出しの単位と表記が合わない | PARTIALLY TRACEABLE | CONFLICTING（単位）／UNKNOWN（総数） | p1, p4, p12, p14, p33 |
| F-24 | MU-30 Group B の一員になった ／ MU-32 会社概要の設立年月 | p34, p36（p16, p14） | Context / Pragmatics | CONTEXT_LOSS | 「一員」の具体的な関係（資本関係等）、Company A との関係が示されていない。設立年月と、事例・導入企業の声・p16 の実績数との時期の関係が示されていない。p14 の画面キャプチャ内の社名は p36 の社名と表記が異なる （Human Review 注記: この Finding には 3 つの所見が含まれている。Test 01-1 で実際に生成された粒度の Evidence として、分割せずに保持する） | PARTIALLY TRACEABLE | UNKNOWN（関係・時期）／CONFLICTING（社名表記） | p14, p16, p34, p36 |
| F-25 | MU-31 AI 教育はあらゆる業界で必要とされ、確実に伸びる市場 | p35 | Commitment | COMMITMENT_ESCALATION | 成果物内の市場データは生成AI市場全体（p6）で、AI 教育市場のデータは示されていない。「あらゆる業界」「確実に」は根拠の範囲を超える強さ | UNTRACEABLE | INFERRED | p6, p35 |
| F-26 | MU-29 営業資料や契約書の雛形で、短期間で開始 | p32（p15） | Evidence → Interpretation | OTHER（成果物内の記述の不一致） | p32 は「契約書の雛形」、p15 は「申込書の雛形」と書いており、提供物の種類が一致しない。p15 の「リーガルチェックの工数削減」の範囲も示されていない | PARTIALLY TRACEABLE | CONFLICTING | p15, p32 |

## 10. Critical Unknowns

| # | Unknown | 影響する Finding | なぜ判定に重要か |
|---|---|---|---|
| 1 | p6 の円建て数値の出典と換算方法 | F-01 | 表示倍率がどの数値に基づくのかが決まらない |
| 2 | Service A の料金体系の全体（月額固定費以外の費用、アカウント利用料の単価、初期費用・契約期間・解約条件） | F-10, F-11, F-12 | シミュレーションとコスト比較の前提であり、「利益」「月額の投資」という提示の範囲が決まらない |
| 3 | 事例の当事者・時期・母数・算定方法 | F-13〜F-16 | 「実績」として提示された数値がどの条件の結果なのか判定できない |
| 4 | 導入企業の声の測定方法・期間と、導入企業と Service A の関係 | F-17, F-18 | 数値が何を測ったものか、誰の成果として読むべきかが決まらない |
| 5 | Company A の設立年月と、事例・導入実績・監修者の実績の時期の関係 | F-13, F-24 | 実績がこの事業によるものか、前身・個人・他社によるものかで意味が変わる |
| 6 | 提供本数・提供数の数え方と、画面キャプチャの件数表示の対象 | F-23 | 提供量の主張の道筋が決まらない |
| 7 | p7 労働人口予測グラフの出典 | F-03 | 数値の出どころが特定できない |
| 8 | 事業者として参加する契約の法的な性質（加盟契約か、再販契約か） | F-13, F-16 | 事例の位置づけと、読み手が負う義務・費用の範囲に関わる |

## 11. Source Verification Required

| # | 確認すべき Source / 事実 | 対象 Meaning Unit | 確認方法の候補 |
|---|---|---|---|
| 1 | Public Source 1 の生成AI市場需要額（各年の値、内訳、年平均増加率） | MU-07 | 出典の公表資料と照合 |
| 2 | 円建て数値の出所と、表示倍率の算出根拠 | MU-08 | 作成者への確認、Public Source 1 内の円建て表記の有無の確認 |
| 3 | 労働人口予測の出典と数値 | MU-09 | 作成者への出典確認、該当統計との照合 |
| 4 | Public Source 3 の IT 人材・AI 人材の不足数とシナリオ | MU-09 | 公表資料と照合 |
| 5 | Public Source 2 の図表・数値・設問と、見出しの趣旨に当たる設問の有無 | MU-10 | 出典の記事・レポートと照合 |
| 6 | 動画・講座の総数、更新頻度、無料で更新される範囲 | MU-13, MU-26 | 作成者への確認、学習管理システム上の一覧、契約書面 |
| 7 | Service A の料金（月額固定費、アカウント利用料の単価、その他の費用） | MU-18〜20, MU-25 | 料金表、契約書面、見積書 |
| 8 | 事例 3 件の当事者と元データ | MU-21〜23 | 作成者への確認、当事者の同意を得た記録 |
| 9 | Client A〜C の実在、発言内容、数値の測定方法、掲載許諾 | MU-24 | 作成者への確認、インタビュー記録・掲載許諾 |
| 10 | 監修者の経歴（実績の数値、役職歴）と監修の実態 | MU-17 | 作成者・本人への確認、公開プロフィール |
| 11 | Group B の会社情報と、Company A / Service A との関係 | MU-30 | Group B の公式開示資料、Company A への確認 |
| 12 | Company A の会社情報（設立年月、資本金など）と、p14 の社名表記 | MU-32, MU-16 | 登記情報、公式 Web サイト、作成者への確認 |
| 13 | 助成金に関する記述（非対応であること、不正受給リスクとの関係） | MU-27 | 作成者への確認、制度の公式情報 |
| 14 | 導入コスト・期間・開始までの日数についての具体的な表現の根拠 | MU-02, MU-04, MU-29 | 作成者への確認、見積・導入実績の記録 |

## 12. Human Review Required

AI が出力した 17 項目です。Human Decision 欄は空欄のままです。R-3〜R-9 の整理は [../review/test-01-1-human-review.md](../review/test-01-1-human-review.md) の 7 にあります。

| # | 対象 Finding | レビューで確認すべき問い | Human Decision |
|---|---|---|---|
| 1 | F-01 | 表示倍率「20倍」はドル建てグラフと円建て数値のどちらに基づくのか。円建て数値の出典は何か | |
| 2 | F-02, F-25 | 生成AI市場全体の数値を AI 研修事業の成長性の根拠に使うことを、読み手が区別できる形で示しているか | |
| 3 | F-03 | p7 左のグラフの出典は何か。出典表記はどの図に係るのか | |
| 4 | F-04 | p8 の見出しは、出典調査のどの設問・結果に対応するのか | |
| 5 | F-05, F-06, F-07 | 「手遅れ」「最も重要」「最も理想的」を支える推論は資料の外にあるか。p10 の円の位置は何に基づくのか | |
| 6 | F-08, F-09, F-19 | 「すべて解決」「開発リスクはゼロ」「陳腐化のリスクはない」の範囲と条件（契約上の保証範囲を含む）は何か | |
| 7 | F-10, F-11 | シミュレーションの前提は何か。p13 の価格の例と異なる単価を使った理由は何か | |
| 8 | F-12 | p29 の「自社で構築した場合」の想定コストの金額と根拠は何か。Service A 側にアカウント利用料などを含めない理由は何か | |
| 9 | F-13, F-14, F-16 | 事例の当事者・時期・母数・算定方法は確認できるか。p23 の分母の社数はどう選ばれたか | |
| 10 | F-15 | p24 のアポ率の改善は Service A の導入によるものか、スクリプトの変更によるものか。比較の期間と件数は何か | |
| 11 | F-17, F-18 | 「受講者の声」と「導入企業の声」の関係、各数値の定義・測定方法は何か | |
| 12 | F-20 | 助成金非対応の説明で「不正受給のリスク」に触れることは、読み手にどんな含意を与えるか | |
| 13 | F-21 | 「最高品質」「監修」の根拠と、経歴中の数値の根拠は何か | |
| 14 | F-22 | 「職種別・業務別」のカリキュラムは、実際の構成と対応しているか | |
| 15 | F-23 | 提供本数・提供数・画面の件数表示は、それぞれ何を数えたものか | |
| 16 | F-24 | 設立年月と実績の時期・主体の関係、Group B との具体的な関係、p14 の社名表記は何か | |
| 17 | F-26 | 提供されるのは契約書の雛形か、申込書の雛形か | |

## 13. Limitations

- Source verification は実施していない
- 成果物内で言及された外部 Source（Public Source 1〜3、Group B、Client A〜C など）の内容は確認しておらず、すべて UNKNOWN として扱った
- 判定はページ画像の読み取りとテキスト層に基づく。画像内の小さな文字（p14 の画面キャプチャ、p6・p8 の注記など）は読み取りを誤っている可能性がある
- 数値の検算は成果物内の数値どうしで行ったもので、数値そのものの正しさは判定していない
- 口頭説明、添付資料、契約書面など、スライドの外で示される可能性のある根拠は考慮していない
- 作成者・作成日・作成手段（AI 生成かどうかを含む）は特定できず、作成過程による Meaning Shift と編集の意図による Meaning Shift を区別していない
- Meaning Unit は Finding に関係する主なものに限っており、すべての記述を列挙してはいない
- 公開版の注記: 固有名詞、原値、長い引用を匿名化・一般化した。原本との意味の一致は Human Review 記録の 6 で照合している
