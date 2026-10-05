# Test 01-1 Human Review Record

- Test: Test 01-1: Presentation Artifact — Generation Provenance Unknown
- Report: [../audit/test-01-1-public.md](../audit/test-01-1-public.md)（公開版。原本は Private Evidence Vault）
- Date: 2026-10-06
- Reviewer: Human Reviewer（リポジトリ管理者）
- 記録作成: Claude Opus 5.5（Human の判断を記録し、判断材料を整理したもの。AI は判断を確定していない）
- **Test 01-1 Status: FROZEN — FIELD EVIDENCE**（2026-10-06）

このテストは、AI 生成プレゼンであることが確認できたテストではありません。生成来歴が不明なプレゼンテーション資料に対して、Artifact-Only の Meaning Audit がどこまで機能するかを観察したフィールドテストです。

---

## 1. Human Review Decisions

### HR-01: Test 01-1 の位置づけ

- 判断: 監査対象はプレゼンテーション資料だが、AI 生成であることは確認できなかった。`AI-Generated Presentation` とは確定せず、Test 01-1 を **Test 01-1: Presentation Artifact — Generation Provenance Unknown** として扱う
- Generation Tool: `UNKNOWN`
- PFC-004（生成過程の来歴）はそのまま維持する
- 影響: Test 01（AI-Generated Presentation）の本来の目的は、Test 01-2 で検証する

### HR-02: Public Repository Policy

- 判断: 今回の目的は第三者企業の公開評価ではなく、Meaning Audit Workflow v1.0 のフィールドテストである。実名入りの Report を公開リポジトリに push しない
- 次の二層構造にする

| 層 | 置き場所 | 内容 |
|---|---|---|
| Private Evidence Layer | 非公開の Evidence Vault（git 管理外） | 元の資料、実名・原値入りの Audit Report と Finding、元の比較レビュー、Source の情報、SHA-256、ページの対応表、匿名化の対応表 |
| Public Test Layer | GitHub | 匿名化・一般化した Audit Report と Finding、Failure Pattern、Post-Freeze Candidate、Test Log、Human Review の結果 |

匿名化の方針: 第三者を直接特定する固有名詞を、Company A、Service A、Group B、Client A〜C、Representative A〜C、Public Source 1〜3 に置き換える。Finding の成立に必要でない原値（金額・割合・件数など）は、概数・桁・関係に一般化する。ページ番号、Finding ID、Status、情報状態は維持する。

---

## 2. Human Review 項目の状況

| # | 対象 | 状況 | Human Decision |
|---|---|---|---|
| R-1 | Test 01 の前提（AI 生成か） | HR-01 で判断済み | Provenance Unknown として扱う |
| R-2 | 公開の可否 | HR-02 で判断済み | 実名入りは非公開。匿名化版のみ公開 |
| R-3〜R-9 | 下の 7・9 と Final Decision Packet | Human Decision 記入済み（2026-10-06） | [test-01-1-final-decision-packet.md](test-01-1-final-decision-packet.md) |
| FP-005 | 下の 3 | 暫定判断済み | 下の 3 のとおり |
| Meaning Preservation | 下の 6 | F-05・F-23 の REVISE を反映し、照合をやり直した（YES 26） | F-05: REVISE ／ F-23: REVISE |

---

## 3. FP-005 の暫定 Human Decision

- 問い: 資料内の数値を検算することは、External Knowledge の導入に当たるか
- 暫定 Human Decision: **成果物内部に存在する数値のみを使った算術的検算は、External Knowledge の導入とはみなさない**
- 理由: 外部 Evidence を追加せず、Artifact 内部の整合性を確認しているため
- 扱い: Workflow v1.0 には反映しない。Workflow 改訂の候補として保持する（[../../../tests/failure-patterns.md](../../../tests/failure-patterns.md) の FP-005 に記録先を追記済み）
- 範囲の注意: この判断は「成果物内の数値のみを使った算術」に限られる。為替レートや制度の知識など、成果物の外の情報を使う検算は対象外

---

## 4. R-6 対象 Finding の再確認

Finding は削除・修正していません。Finding 原文は公開版（一般化後）の表現です。Human Decision 欄は空欄です。

### F-14

| 項目 | 内容 |
|---|---|
| Finding 原文（公開版） | 成約率の分母（小さな社数）は「興味を持つ顧客にだけ案内する」という施策の記述と並び、事前に絞られた母数である可能性がある。単価・期間・当事者は示されていない |
| Status / 情報状態 | UNTRACEABLE / INFERRED（母数の性質）・UNKNOWN（その他） |
| Artifact から確認できること | p23 に分数で示された成約率があること。施策欄に「興味を持つ顧客にだけ案内する」趣旨の記述があること。単価・期間・当事者の記載が無いこと |
| Inference が始まる地点 | 施策欄の記述と成約率の分母を結びつけるところ。資料は分母の社がどう選ばれたかを述べていない |
| Finding Type の妥当性 | 要確認。「母数の選び方によって成約率の意味が変わる」に焦点を当てれば SELECTION だが、「母数の選び方が示されていない」に焦点を当てれば INFERENCE_GAP とも読める |
| Status の妥当性 | 妥当。成約率の根拠（当事者・期間・母数）は成果物内に無く、UNTRACEABLE は推測部分に依存しない |
| 1 Finding に複数の所見 | あり（2 つ）: (a) 母数が絞り込まれている可能性（INFERRED）、(b) 単価・期間・当事者が示されていないこと（確認できる） |
| Human Decision | |

### F-20

| 項目 | 内容 |
|---|---|
| Finding 原文（公開版） | 非対応という制約を、助成金の利用と「不正受給のリスク」を結びつけることで利点として提示している。「即決しやすく利益に直結」の因果の根拠は示されていない |
| Status / 情報状態 | UNTRACEABLE / INFERRED |
| Artifact から確認できること | p31 の FAQ で、助成金非対応の説明の中に「審査の手間や不正受給のリスクを避け」という趣旨の記述があること。「即決しやすく利益に直結」の根拠が書かれていないこと |
| Inference が始まる地点 | 「不正受給のリスク」への言及が、助成金を使う選択肢を不利に見せる効果を持つ、という表現の効果についての解釈 |
| Finding Type の妥当性 | 要確認。主な内容を Framing の解釈とするなら FRAMING、根拠の無い因果（即決しやすく利益に直結）とするなら INFERENCE_GAP または CAUSAL_IMPLICATION |
| Status の妥当性 | 妥当。因果の根拠が成果物内に無いことは確認できる |
| 1 Finding に複数の所見 | あり（2 つ）: (a) 制約を利点に見せる Framing（INFERRED）、(b) 因果の根拠の欠落（確認できる） |
| Human Decision | |

### F-22

| 項目 | 内容 |
|---|---|
| Finding 原文（公開版） | p14 のレッスン名はツール・機能別が中心で、p1 のカテゴリも同様。「職種別・業務別」の構成は成果物の中では確認できない（p14 に業務別の講座が 1 件ある）。「高単価で提案できる」の根拠も無い |
| Status / 情報状態 | PARTIALLY TRACEABLE / INFERRED |
| Artifact から確認できること | p14 の 1 講座のレッスン名、p1 の画面に見えるカテゴリ、p32 の「職種別・業務別」の記述、「高単価」の根拠が無いこと |
| Inference が始まる地点 | p14 の 1 講座と p1 の画面から、カリキュラム全体の構成を推し量るところ。資料に見えているのは全体の一部だけ |
| Finding Type の妥当性 | 妥当（INFERENCE_GAP）。「差別化できる」「高単価で提案できる」への根拠が示されていない点は推論の欠落 |
| Status の妥当性 | 要確認。見えている範囲だけでは判定できないとすれば、UNKNOWN の方が適切な可能性がある。現在の PARTIALLY TRACEABLE は「一部の根拠（業務別の講座 1 件）がある」と読んだもの |
| 1 Finding に複数の所見 | あり（2 つ）: (a) 「職種別・業務別」の構成の確認、(b) 「高単価」の根拠の欠落 |
| Human Decision | |

### F-24

| 項目 | 内容 |
|---|---|
| Finding 原文（公開版） | 「一員」の具体的な関係、Company A との関係が示されていない。設立年月と事例・導入企業の声・実績数との時期の関係が示されていない。p14 の画面キャプチャ内の社名は p36 の社名と表記が異なる |
| Status / 情報状態 | PARTIALLY TRACEABLE / UNKNOWN（関係・時期）・CONFLICTING（社名表記） |
| Artifact から確認できること | p36 の設立年月、p34 の「グループの一員」の記述、p14 の画面キャプチャ内の社名表記が p36 と異なること |
| Inference が始まる地点 | 設立年月と実績の時期の関係を取り上げるところ（実績がこの会社のものだという前提を置いている）。前身事業、個人の実績、グループ会社の実績、デモ環境の表示である可能性は、成果物の外の情報で判断できない |
| Finding Type の妥当性 | 要確認。社名表記の違いは成果物内の不整合（PFC-003 の対象）で、CONTEXT_LOSS での代用。グループとの関係の欠落は CONTEXT_LOSS として読める |
| Status の妥当性 | 要確認。所見ごとに状態が異なり（UNKNOWN と CONFLICTING）、1 つの Status にまとめることが難しい |
| 1 Finding に複数の所見 | あり（3 つ）: (a) Group B との関係、(b) 設立時期と実績の時期の関係、(c) 社名表記の違い |
| Human Decision | |

観察（Workflow には反映しない）: R-6 の 4 件はすべて、1 つの Finding に複数の所見が入っている。Finding の粒度は FP-002（1 Finding に複数の情報状態）と FP-006（Report の粒度）に関係する。新しい Failure Pattern としては登録せず、Test 01-2 で再び観察されるかを確認する。

---

## 5. Public / Private の境界

Private Evidence Layer は、このリポジトリとは別の非公開の Evidence Vault（git 管理外）に保管しています。Test ごとに同じ構成を使います。

| Vault 内の場所 | 内容 |
|---|---|
| `test-01-1/source/` | 元の資料（第三者の著作物。ファイル名・内容は無変更） |
| `test-01-1/private-audit/` | AI が出力した Report の原本（実名・原値入り・無編集） |
| `test-01-1/review/` | 匿名化する前の比較レビュー・Test 記録 |
| `test-01-1/metadata/` | manifest（SHA-256、ページ数、権利・公開の扱い、関連記録）、ページの対応表、匿名化の対応表 |

公開リポジトリにあるもの:

| ファイル | 内容 |
|---|---|
| [../audit/test-01-1-public.md](../audit/test-01-1-public.md) | 匿名化・一般化した Report |
| [mode-comparison.md](mode-comparison.md) | 匿名化・一般化した比較レビュー |
| この文書 | Human Review の記録 |

元の資料は、公開リポジトリにコピー・commit・push しません。`.gitignore` の `private/` は、ローカルで誤ってコミットするのを防ぐために残しています。

---

## 6. Meaning Preservation Review（公開版と原本の照合）

公開版（匿名化・一般化後）と Private Vault の原本を、Finding ごとに照合しました。再監査ではなく、匿名化・一般化で意味が変わっていないかの確認です。照合は AI が行ったもので、Human の確認が必要です。

### 照合の範囲

| 対象 | 結果 |
|---|---|
| Claim（Meaning Unit の趣旨） | 一致。原値と特徴的な言い回しを趣旨に言い換えた |
| Finding（内容欄） | 下の表のとおり |
| Status | 26 件すべて一致（変更なし） |
| Meaning Trace | 7 件すべて Stage 構成・Status が一致。KS-1 の見出しを、原本の固有の表現から「表示倍率」に一般化した |
| Information State | 26 件すべて一致（変更なし） |
| Human Review Required | 17 項目、問いの趣旨が一致 |

### Finding ごとの照合

| Finding ID | Meaning Preserved | Difference | Human Review Needed |
|---|---|---|---|
| F-01 | YES | 金額の原値を削除。「計算上は約 15 倍、表示は 20 倍、ドル建ては約 20 倍」という関係は維持 | NO |
| F-02 | YES | なし | NO |
| F-03 | YES | シナリオ名と不足数の原値を削除。「異なるシナリオ名が並ぶ」「見出しの年と不足数の年が異なる」は維持 | NO |
| F-04 | YES | 割合の原値と見出しの年数を削除。「増加幅は確信の方が大きい」「見出しの年数・語はグラフに無い」は維持 | NO |
| F-05 | YES | 2026-10-06 に REVISE を反映。公開版は画像の観察（Visual observation: こぼれた硬貨と排水口が写っている）と解釈（損失回避の Framing）を分けて書く形に戻した。企業を特定する情報は含まない | NO |
| F-06 | YES | なし | NO |
| F-07 | YES | なし | NO |
| F-08 | YES | なし | NO |
| F-09 | YES | 「最短○週間」など一部の具体表現を一般化 | NO |
| F-10 | YES | 利益額の原値と、逆算した単価の値を削除。「見出しの合計は表と整合」「単価は逆算」は維持 | NO |
| F-11 | YES | なし | NO |
| F-12 | YES | 月額固定費の原値を削除 | NO |
| F-13 | YES | 売上・粗利率・期間を「短期間」「数百万円規模」「高い粗利率」に一般化。根拠の欠落という Finding の要点は維持 | NO |
| F-14 | YES | 成約率の原値を「分数で示された成約率」「小さな社数」に一般化。母数の性質の推測（INFERRED）は維持 | NO |
| F-15 | YES | アポ率と倍率の原値を削除。「倍率は前後の値と整合」「帰属のずれ」は維持 | NO |
| F-16 | YES | なし | NO |
| F-17 | YES | なし | NO |
| F-18 | YES | 6 指標の原値と、意味を特定できないラベルの原文を削除。「2 件は整合、4 件は定義なし」の構造は維持 | NO |
| F-19 | YES | なし | NO |
| F-20 | YES | なし | NO |
| F-21 | YES | 経歴中の数値の原値を削除 | NO |
| F-22 | YES | 具体的なツール名を、ツールの種類（画像生成、動画生成など）に一般化 | NO |
| F-23 | YES | 2026-10-06 に REVISE を反映。公開版 KS-7 から、原本に無かった「提供本数より少ない」という比較を除き、原本と同じく「1 講座分の動画本数の合計を検算で求めた」だけを書く形に戻した（原値は Private） | NO |
| F-24 | YES | 所在地の原文を削除。「Group B と Company A の所在地が同じ表記」という観察は KS-7 の Meaning Trace に維持 | NO |
| F-25 | YES | なし | NO |
| F-26 | YES | なし | NO |

結果: YES 26 件、UNCERTAIN 0 件、NO 0 件（2026-10-06、F-05・F-23 の修正後に更新。修正前は YES 24 件、UNCERTAIN 2 件）。

**再照合（2026-10-06、R-3〜R-9 の Human Decision 反映後）**: 照合の基準を「Private 原本 ＋ Human Decision」とした。F-12・F-14・F-20・F-22 は Human Decision どおりに原本から意図して変更したもので、その変更内容が Decision と一致することを確認した。F-24 は内容を変えず注記のみ。その他の 21 件は前回の照合から変更なし。結果: YES 26 件、UNCERTAIN 0 件、NO 0 件。

---

## 7. R-3〜R-9 の整理

AI Recommendation は判断材料の整理であり、Human Decision ではありません。分類: `ACCEPT` / `REVISE` / `HOLD` / `INVESTIGATE` / `NO ACTION`。

| # | 対象 | Current Issue | Evidence | AI Recommendation | Human Decision |
|---|---|---|---|---|---|
| R-3 | F-01 | 表示倍率「20倍」の不一致は、円建て数値の側の問題として読むのが妥当か | 主セッションが p6 の画像を直接確認した。ドル建ての倍率は約 20 倍、円建ての倍率は約 15 倍で、Ledger はこの区別を保っている。KS-1 の要約では区別が弱い | ACCEPT（Finding は成果物内の検算だけで成り立つ。KS-1 の要約表現は Test 01-1 を Freeze したうえで記録にとどめる） | |
| R-4 | F-04 | 見出しとグラフのずれ（Title-body）の判定は妥当か | 主セッションが p8 の画像を直接確認した。見出しの年数・語はグラフに無く、2 時点の比較である | ACCEPT（見出しとグラフが同じページにあり、成果物内で確認できる。Source の設問との対応は Run 01A の範囲） | |
| R-5 | F-07, F-12 | Visual Claim の解釈（象限図の円の配置、目盛りの無い比較の棒）は妥当か | F-07: p10 に配置の根拠となるデータが無い（確認できる）。F-12: 主セッションが p29 を直接確認し、比較対象に金額・目盛りが無いことを確認した。ただし F-12 の情報状態 CONFLICTING は、食い違いというより費用範囲の不提示とも読める | F-07: ACCEPT ／ F-12: REVISE（Finding の内容は維持し、情報状態 CONFLICTING の妥当性を確認する） | |
| R-6 | F-14, F-20, F-22, F-24 | 推測が強すぎる可能性 | 上の 4 のとおり。4 件とも 1 つの Finding に複数の所見が入っている | F-14: HOLD（推測部分は INFERRED と明記されており、Status は推測に依存しない）／ F-20: REVISE（Framing の解釈と因果の欠落を分けるか確認する）／ F-22: REVISE（Status を UNKNOWN とするか確認する）／ F-24: HOLD（複数の所見の扱いは Workflow 全体の論点で、Test 01-2 の結果を待つ） | |
| R-7 | F-03, F-18 | Source との対応が曖昧な箇所 | F-03: 出典表記がどの図に係るかは、Public Source 3 を見れば確かめられる可能性がある。F-18: 導入企業の数値の定義は Client A〜C の測定記録が必要で、入手できる見込みが低い | F-03: INVESTIGATE（公開統計で確認できる）／ F-18: HOLD（Source の入手手段が無い） | |
| R-8 | Run 01A | Test 01-1 で Run 01A を実行するか | Source が無い。公開統計（Public Source 1〜3）だけで p6〜p8 の部分的な Mode A は可能だが、資料全体の Source ではない | NO ACTION（Test 01-1 は Mode B の単独記録として Freeze し、Mode A と B の比較は Test 01-2 で行う） | |
| R-9 | Report 全体 | Finding 26 件、Human Review 17 項目という粒度は運用上適切か | FP-006 に記録済み。R-6 の 4 件はすべて 1 Finding に複数の所見を含む | HOLD（FP-006 のフィールド Evidence として保持し、Test 01-2 の粒度と比べてから判断する） | |

---

## 8. Freeze Readiness

| 条件 | 状態 | 根拠 |
|---|---|---|
| Private Evidence を非公開の Evidence Vault へ移行済み | 達成 | Vault の `test-01-1/` に、元の資料と原本の記録 9 ファイル。manifest に SHA-256 を記録し、移動の前後でハッシュ値が一致 |
| Public / Private の境界が明確 | 達成 | 上の 5 |
| Public 版の再特定リスクを低減済み | 達成（注記あり） | 原値を一般化し、2026-10-06 に git の履歴も書き換えた（main の全履歴で原値 0 件）。書き換え前のコミットの扱いについての Human Decision は Private の記録にある |
| Public 版と Private 版の Meaning Preservation を確認済み | 達成 | 上の 6（YES 26、F-05・F-23 は Human Decision REVISE を反映） |
| R-3〜R-9 を整理済み | 達成（Human Decision 記入済み） | 上の 7・9、Final Decision Packet |
| FP-001〜006 を記録済み | 達成 | [../../../tests/failure-patterns.md](../../../tests/failure-patterns.md) |
| PFC-003・004 を記録済み | 達成 | [../../../tests/post-freeze-candidates.md](../../../tests/post-freeze-candidates.md) |
| 公開リポジトリに Private Evidence が無い | 達成 | push 前の安全確認と、GitHub 側のファイル一覧の確認 |
| Workflow / Prompt 本体を変更していない | 達成 | 該当 6 ファイルの最終更新は初期構築のコミット |

```text
Test 01-1 Status（Freeze 前）:
FREEZE CANDIDATE — HUMAN REVIEW REQUIRED
```

2026-10-06、下の Human Decision がすべてそろったため、Freeze しました（下の 10）。

- ~~6 の UNCERTAIN 2 件（F-05, F-23）~~ → Human Decision REVISE を反映済み
- 7 の R-3〜R-9
- ~~書き換え前のコミットの扱い~~ → Human Decision 済み（Private の記録）

未決事項の詳細は下の 9 にまとめています。R-3〜R-9 は [test-01-1-final-decision-packet.md](test-01-1-final-decision-packet.md) で判断できるようにまとめています。

---

## 9. Final Freeze Review（未決事項の整理）

2026-10-06、git 履歴の書き換え後に整理しました。AI Recommendation は 7 の内容を維持しており、Human Decision ではありません。Human Decision 欄は空欄です。

### F-05

**Current Issue**
公開版で画像の具体的な描写を「損失を連想させる写真」と一般化したため、Visual Claim の解釈が一段加わった可能性がある（6 の UNCERTAIN）。

**Existing Evidence**

| 観点 | Private 原本 | Public 版 |
|---|---|---|
| Visual Claim（KS-3 Context / Pragmatics） | 画像の具体的な描写（何が写っているか）を書いたうえで、「損失回避の Framing を形成する」と述べる | 「損失を連想させる写真と…で損失回避の Framing をつくる」 |
| Finding Ledger（F-05） | 「画像（具体的な描写）で強められている」 | 「画像で強められている」 |
| Status / 情報状態 | UNTRACEABLE / UNKNOWN | UNTRACEABLE / UNKNOWN（同じ） |

- 主セッションが p9 の画像を直接確認した。原本の描写（硬貨が容器からこぼれ、路面の排水口の近くに散らばり、手が伸びている）は画像と一致する
- 「損失回避の Framing」という解釈は原本にもある。公開版で加わったのは、描写（何が写っているか）を省いて解釈（損失を連想させる）だけを書いた点で、読み手が描写から解釈を検証できなくなっている
- 参考: Skill 互換性確認の実行では、同じ写真の読み取りを INFERRED としていた。原本 Run 01B は写真の読み取りに情報状態を付けていない

**Meaning Preservation**: Finding の結論（根拠なしの損失回避 Framing、UNTRACEABLE）は維持されている。描写から解釈への段階は公開版で圧縮されている。

**Interpretation の追加**: あり（描写の省略によって、解釈が描写の代わりに置かれた）。ただし解釈そのものは原本と同じ。

**AI Recommendation**: REVISE（公開版の KS-3 の表現を、描写と解釈を分けた形に戻すかを検討する。例: 「硬貨がこぼれて排水口の近くに散らばる写真（描写）」と「損失回避の Framing（解釈、INFERRED）」。描写には企業を特定する情報は含まれない）

**Possible Human Decisions**: ACCEPT / REVISE / HOLD / INVESTIGATE / NO ACTION

**Human Decision**: REVISE（2026-10-06。公開版に反映済み）

### F-23

**Current Issue**
公開版の KS-7 の Meaning Trace が、原本より不一致を強く読ませる可能性がある（6 の UNCERTAIN）。

**Existing Evidence**

| 観点 | Private 原本 | Public 版 |
|---|---|---|
| Meaning Trace（KS-7 Interpretation） | 「本」「種類」と単位が揺れる。p14 の 1 講座の動画本数の合計を検算で示す（値のみ。提供数との比較はしない）。画面の件数表示の対象は UNKNOWN | 「本」「種類」と単位が揺れる。「1 講座分の動画本数の合計は、表示された提供本数より少ない（KNOWN: 検算）」。画面の件数表示の対象は UNKNOWN |
| Finding Ledger（F-23） | 1 講座の合計と画面の件数表示が、提供数とどう関係するか示されていない | 同じ趣旨 |
| Status / 情報状態 | PARTIALLY TRACEABLE / CONFLICTING（単位）・UNKNOWN（総数） | 同じ |

- Claim strength: 公開版の「提供本数より少ない」は、1 講座の合計と全体の提供数を比べる形になっている。1 講座の本数が全体より少ないことは不一致を意味しないが、並べ方によっては不一致の根拠のように読める。原本はこの比較をしていない
- Finding strength: Ledger の Finding は原本と同じ（関係が示されていない）。強く読ませる可能性があるのは Meaning Trace の 1 文だけ
- Status: 変化なし

**AI Recommendation**: REVISE（公開版 KS-7 の該当文を、原本と同じく比較をしない表現にするかを検討する。例: 「p14 の表から 1 講座分の動画本数の合計は算出できるが、表示された提供数との関係は示されていない」）

**Possible Human Decisions**: ACCEPT / REVISE / HOLD / INVESTIGATE / NO ACTION

**Human Decision**: REVISE（2026-10-06。公開版に反映済み）

### R-3（F-01）

**Current Issue**: 表示倍率「20倍」の不一致を、円建て数値の側の問題として読むのが妥当か。KS-1 の要約では区別が弱い。
**Existing Evidence**: p6 を直接確認した。ドル建ての倍率は約 20 倍、円建ての倍率は約 15 倍。Ledger はこの区別を保っている。Skill 互換性確認の実行でも同じ読み方だった（S-06）。
**AI Recommendation**: ACCEPT
**Possible Human Decisions**: ACCEPT / REVISE / HOLD / INVESTIGATE / NO ACTION
**Human Decision**: ACCEPT（2026-10-06）

### R-4（F-04）

**Current Issue**: 見出しとグラフのずれ（Title-body）の判定は妥当か。
**Existing Evidence**: p8 を直接確認した。見出しの年数・語はグラフに無く、2 時点の比較である。Skill 互換性確認の実行でも同じ Finding（S-09）。
**AI Recommendation**: ACCEPT
**Possible Human Decisions**: ACCEPT / REVISE / HOLD / INVESTIGATE / NO ACTION
**Human Decision**: ACCEPT（2026-10-06）

### R-5（F-07, F-12）

**Current Issue**: Visual Claim の解釈（象限図の円の配置、目盛りの無い比較の棒）は妥当か。F-12 の情報状態 CONFLICTING は妥当か。
**Existing Evidence**: F-07: p10 に配置の根拠データが無い。F-12: p29 を直接確認し、比較対象に金額・目盛りが無いことを確認した。F-12 の CONFLICTING は、食い違いというより費用範囲の不提示とも読める。Skill 互換性確認の実行は、F-12 に当たる内容を 2 件に分けた（S-22: UNKNOWN、S-23: KNOWN）。
**AI Recommendation**: F-07 → ACCEPT ／ F-12 → REVISE
**Possible Human Decisions**: ACCEPT / REVISE / HOLD / INVESTIGATE / NO ACTION
**Human Decision**: F-07: ACCEPT ／ F-12: REVISE（2026-10-06、公開版に反映済み）

### R-6（F-14, F-20, F-22, F-24）

**Current Issue**: 推測が強すぎる可能性。4 件とも 1 つの Finding に複数の所見を含む。
**Existing Evidence**: 4 の整理（Artifact から確認できること、Inference が始まる地点、Finding Type と Status の妥当性、複数の所見）。Skill 互換性確認の実行では、F-14 に当たる Finding は母数の推測をしていない（S-18）。F-24 に当たる内容は 2 件に分かれた（S-28, S-30）。
**AI Recommendation**: F-14 → HOLD ／ F-20 → REVISE ／ F-22 → REVISE ／ F-24 → HOLD
**Possible Human Decisions**: ACCEPT / REVISE / HOLD / INVESTIGATE / NO ACTION
**Human Decision**: F-14: REVISE ／ F-20: REVISE ／ F-22: REVISE（いずれも公開版に反映済み） ／ F-24: HOLD（3 つの所見を含むという注記を維持し、分割しない）（2026-10-06）

### R-7（F-03, F-18）

**Current Issue**: Source との対応が曖昧な箇所。
**Existing Evidence**: F-03: 出典表記がどの図に係るかは、Public Source 3 を見れば確かめられる可能性がある。F-18: 導入企業の数値の定義は Client A〜C の測定記録が必要で、入手の見込みが低い。
**AI Recommendation**: F-03 → INVESTIGATE ／ F-18 → HOLD
**Possible Human Decisions**: ACCEPT / REVISE / HOLD / INVESTIGATE / NO ACTION
**Human Decision**: F-03: NO ACTION（Test 01-1 は Artifact-Only Audit として閉じ、Evidence Boundary を後から広げない） ／ F-18: HOLD（UNKNOWN / Source Verification Required のまま保持）（2026-10-06）

### R-8（Run 01A）

**Current Issue**: Test 01-1 で Run 01A（Source-Grounded）を実行するか。
**Existing Evidence**: 資料全体の Source は無い。公開統計（Public Source 1〜3）だけで p6〜p8 に限った Mode A は可能。Mode A と B の比較は Test 01-2 で設計済み。
**AI Recommendation**: NO ACTION
**Possible Human Decisions**: ACCEPT / REVISE / HOLD / INVESTIGATE / NO ACTION
**Human Decision**: NO ACTION（2026-10-06。Mode 比較は Test 01-2 で行う）

### R-9（Report の粒度）

**Current Issue**: Finding 26 件、Human Review 17 項目という粒度は運用上適切か。
**Existing Evidence**: FP-006 に記録済み。R-6 の 4 件はすべて複数の所見を含む。Skill 互換性確認の実行では Finding 30 件で、まとめ方・分け方に差が出た。
**AI Recommendation**: HOLD
**Possible Human Decisions**: ACCEPT / REVISE / HOLD / INVESTIGATE / NO ACTION
**Human Decision**: HOLD（2026-10-06。粒度のばらつきは Field Evidence として保持し、Test 01-1 だけを根拠に Workflow・Prompt を変えない）

---

## 10. Freeze

```text
Test 01-1 Status:
FROZEN — FIELD EVIDENCE
```

- Date: 2026-10-06
- 根拠: R-3〜R-9 の Human Decision（[test-01-1-final-decision-packet.md](test-01-1-final-decision-packet.md)）、F-05・F-23 の Human Decision、Meaning Preservation の再照合（YES 26）、公開リポジトリの安全確認

### FROZEN — FIELD EVIDENCE の意味

次のものを Field Evidence として固定したことを意味します。

- このテストで起きたこと
- AI の Audit Report
- Human Review
- Finding の修正（F-05、F-12、F-14、F-20、F-22、F-23）
- 失敗の観察（FP-001〜FP-006）
- Unknown（Generation Provenance UNKNOWN、Run 01A 未実行、Critical Unknowns）

次のことは意味しません。

- Workflow v1.0 が validated された
- Finding が普遍的に正しい
- AI Audit の再現性が保証された
- Method が final である

### 公開履歴についての Human Decision の更新

- 書き換え前のコミットを指す SHA の文字列が、公開リポジトリの過去の版の記述に残っており、そこから書き換え前のコミットへ直接到達できることが確認された。前回の判断の前提の一部が変わったため、Human Decision を **REMOVE PUBLIC DISCOVERY PATH** に更新した
- 2026-10-06、git filter-repo で該当する文字列を公開履歴から除き、force-with-lease で push した。Public repository history から旧コミットへの公開上の発見経路を除去した
- GitHub 内部に、参照されないオブジェクトが物理的に残っている可能性はある。GitHub Support への削除依頼はしていない。完全に削除されたとは記録しない

### Freeze 時点で維持したもの

FP-001〜FP-006、PFC-003、PFC-004、Skill Runtime Variance Observation、Generation Provenance UNKNOWN、Run 01A 未実行。Workflow v1.0、Prompt、Meaning Audit Skill、Finding Type 体系は変更していない。

