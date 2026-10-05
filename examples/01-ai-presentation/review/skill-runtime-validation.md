# Meaning Audit Skill: Runtime and Variance Validation

- Date: 2026-10-06
- 位置づけ: `skills/meaning-audit` は Meaning Audit Workflow v1.0 の installable implementation。実行ごとに同じ結果を出す監査エンジンではない
- Workflow: v1.0（変更なし）
- Status: AI による記録。Human Review 未実施
- 匿名化: 監査対象は Test 01-1 と同じ第三者の資料のため、公開版 Report と同じ方針で、固有名詞は匿名化し、原値は一般化している。各 Run の Report 原本は Private Evidence Vault に保管

---

## 1. Human Review Decisions（Skill 初期実装）

| ID | 内容 | Human Decision |
|---|---|---|
| SC-1 | Workflow Compatibility | **ACCEPT**。Skill は **Workflow compatible** として扱う。**output equivalent** とは表現しない。Report 構造、Audit Mode、Evidence Boundary、Unknown Policy、禁止事項、Human Review の扱いは一致したが、Finding には差があった（Run 01B の 26 件に対し、一致 21・一部一致 4・未検出 1、Skill 側のみ 4） |
| SC-2 | Repeated Run Test | **ACCEPT**。同じ入力・同じ Skill・同じ依頼で、追加 2 回（S2, S3）を実行する |
| SC-3 | Finding Differences | **HOLD**。Skill 側のみの 4 件、Run 01B のみの F-26、Finding Type・Status・粒度の差は、Workflow 変更の材料にしない。**Run Variance / Compatibility Delta** として記録し、正解・不正解は判定しない |
| SC-4 | Standalone Skill References | **REVISE**。Skill 単体で存在しないリポジトリ内パスへの参照を解消する。修正は `skills/meaning-audit/` 配下だけで、Canonical Workflow は変更しない |

承認された Skill 固有の運用上の指示（SKILL.md に記載）:

| # | 内容 |
|---|---|
| A | テキスト層で読めない重要な情報がある場合、利用できればページ画像・Visual 情報を確認する |
| B | Evidence Boundary の外の情報を、ユーザーの許可なく追加しない。ユーザーが外部検索・取得を Evidence として明示的に許可した場合は、その範囲を Boundary に含めて記録し、利用できる |
| C | ユーザーが保存を求めた場合だけ、Report をファイルとして保存する |
| D | Report の Prompt 欄に `skill: meaning-audit` と記録する |

---

## 2. Skill version と実行環境

| 項目 | 内容 |
|---|---|
| Variance Test（S1〜S3）で使った Skill | コミット `99754ed` 時点の `skills/meaning-audit`（S2・S3 は同じ版のスナップショットを使用し、S1 と条件をそろえた） |
| Runtime Test で使った Skill | コミット `6390b37`（Packaging Revision 後）。Personal Skill として `~/.claude/skills/meaning-audit/` にインストール |
| Claude Code | 2.1.196（Windows 11） |
| 監査モデル | Claude Opus 5.5 |
| Variance Test の実行方法 | この会話の文脈を持たない subagent。読めるのは Skill のファイル、ページ画像、テキスト層だけ。Web 検索なし。過去の Run の結果は見せていない |
| Runtime Test の実行方法 | `claude -p`（ヘッドレス）を新しいセッションとして起動。使えるツールは Read / Skill / Glob に限定 |

---

## 3. Runtime Test（実際の Claude Code へのインストール）

### 3.1 インストール

- `~/.claude/skills/meaning-audit/` には既存の Skill が無かった。上書きなしでコピーし、リポジトリの版と同一であることを確認した
- 新しいセッションの初期化情報で、`meaning-audit` が Skill と slash command の一覧に現れた
- README のインストール手順（個人用 Skill へのコピー）で問題は無かった

### 3.2 テスト文書

Skill の動作確認用に作った架空の提案書（約 15 行。「アンケートの一部の回答 → 全社の課題」「市場の成長 → 取り残される」「効果の断定」「確実・直ちに導入すべき」という Meaning Shift を含む）。実在の資料・数値は使っていない。

### 3.3 Explicit Invocation（`/meaning-audit`）

| 確認項目 | 結果 |
|---|---|
| Skill が認識される | YES。slash command として認識された |
| Meaning Audit として実行される | YES。Skill の references（output-format、finding-types）を読んでから監査した |
| Mode を判定する | YES。Mode B。定型文あり |
| 標準 Report 構造 | YES。13 セクション、Finding 7 件、Prompt 欄は `skill: meaning-audit` |

注: 最初の試行は Git Bash から `claude -p "/meaning-audit ..."` を実行したため、Git Bash のパス変換によって `/meaning-audit` がファイルパスに書き換えられ、slash command として渡らなかった（この試行でも、Claude は依頼文から Skill を選んで実行した）。PowerShell から実行し直し、slash command として正常に動いた。Claude Code の対話画面で使う場合には関係しない。

### 3.4 Natural-Language Invocation

依頼文: 「この提案書（test-proposal.md）をMeaning Auditしてください。」（Skill 名・slash command を指定しない）

| 確認項目 | 結果 |
|---|---|
| Skill が選択される | YES。Claude が Skill ツールで `meaning-audit` を選んだ |
| 標準 Report 構造 | YES。13 セクション、Mode B と定型文、Finding 7 件、Key Meaning Shift 5 件 |
| Human Decision | 空欄（「人間が記入」） |
| 保存 | 会話に出力し、保存は「ご希望なら場所を指定ください」と確認した（運用指示 C どおり） |

「意味の監査」という依頼文での自動選択は試していない。

---

## 4. Variance Test（4 Run の比較）

### 4.1 Run の概要

| Run | 指示 | Finding | KS | TRACEABLE | PARTIALLY | UNTRACEABLE | UNKNOWN | Document Class |
|---|---|---|---|---|---|---|---|---|
| Original Run 01B | `prompts/artifact-only-audit.md` | 26 | 7 | 0 | 14 | 12 | 0 | A（主）/ C（副） |
| Skill Run S1 | Skill | 30 | 7 | 1 | 18 | 9 | 2 | C（主）/ A（副） |
| Skill Run S2 | Skill | 28 | 7 | 0 | 18 | 8 | 2 | C（主）/ A（副） |
| Skill Run S3 | Skill | 31 | 7 | 1 | 16 | 12 | 2 | C（主）/ A（副） |

4 Run とも、Mode B の判定と定型文、13 セクション、Mode B の Status だけを使うこと、誤りの断定・修正案・点数が無いこと、Human Decision 欄が空欄であることは一致した。

### 4.2 Finding cluster

Finding 番号ではなく、意味的に同じ指摘を cluster（C-xx）としてまとめた。○ は出現、△ は他の cluster の中に含まれる形で出現。

| Cluster | 内容（一般化） | 01B | S1 | S2 | S3 | 出現 |
|---|---|---|---|---|---|---|
| C-01 | p6 円建て数値と表示倍率の不一致 | ○ | ○ | ○ | ○ | 4/4 |
| C-02 | 生成AI市場全体から研修事業への Warrant 欠落 | ○ | ○ | ○ | ○ | 4/4 |
| C-03 | p7 出典・シナリオ・年の扱い | ○ | ○ | ○ | ○ | 4/4 |
| C-04 | p8 見出しとグラフのずれ | ○ | ○ | ○ | ○ | 4/4 |
| C-05 | p9「手遅れ」の根拠なき結論 | ○ | ○ | ○ | ○ | 4/4 |
| C-06 | p5「最も重要な理想的条件」 | ○ | ○ | ○ | ○ | 4/4 |
| C-07 | p10 象限図の配置の根拠 | ○ | ○ | ○ | ○ | 4/4 |
| C-08 | 「すべて解決」 | ○ | ○ | ○ | ○ | 4/4 |
| C-09 | 「開発リスクはゼロ」とコスト・期間の根拠 | ○ | ○ | ○ | ○ | 4/4 |
| C-10 | シミュレーションの前提が示されない | ○ | ○ | ○ | ○ | 4/4 |
| C-11 | p29 コスト比較（金額・目盛りの無い比較） | ○ | ○ | ○ | ○ | 4/4 |
| C-12 | p22 事例の根拠欠落 | ○ | ○ | ○ | ○ | 4/4 |
| C-13 | p23 成約率・「一言の提案」 | ○ | ○ | ○ | ○ | 4/4 |
| C-14 | p24 施策と成果の帰属 | ○ | ○ | ○ | ○ | 4/4 |
| C-15 | 「受講者の声」と「導入企業の声」 | ○ | ○ | ○ | ○ | 4/4 |
| C-16 | 導入企業の数値指標の定義 | ○ | ○ | ○ | ○ | 4/4 |
| C-17 | 「陳腐化のリスクはない」 | ○ | ○ | ○ | ○ | 4/4 |
| C-18 | 助成金非対応の Framing | ○ | ○ | ○ | ○ | 4/4 |
| C-19 | 「最高品質」と監修者の経歴 | ○ | ○ | ○ | ○ | 4/4 |
| C-20 | 提供数の表記の不一致 | ○ | ○ | ○ | ○ | 4/4 |
| C-21 | Group B との関係・継続性 | ○ | ○ | ○ | ○ | 4/4 |
| C-22 | 設立時期と実績の時期の関係 | △ | ○ | ○ | ○ | 4/4 |
| C-23 | 「確実に伸びる市場」 | ○ | ○ | ○ | ○ | 4/4 |
| C-24 | p7 棒の高さと数値ラベルの見え方（目視による推定） | | ○ | ○ | ○ | 3/4 |
| C-25 | 利益額の強調と免責注記の小ささ | ○ | ○ | | ○ | 3/4 |
| C-26 | 「職種別・業務別」の構成 | ○ | ○ | ○ | | 3/4 |
| C-27 | 雛形の種類の不一致（p15 と p32） | ○ | | ○ | | 2/4 |
| C-28 | 資料全体の物語構成（ページ順による意味の付加） | | | ○ | ○ | 2/4 |
| C-29 | 画面キャプチャ内の社名表記 | △ | | | | 1/4 |
| C-30 | 事例の見出し「未経験」と Before 欄の経歴 | | ○ | | | 1/4 |
| C-31 | 「専門知識不要」の前提と提供形態 | | ○ | | | 1/4 |
| C-32 | 技術サポートの範囲の記述 | | ○ | | （関連あり） | 1/4 |
| C-33 | p2「よくある悩み」の根拠 | | | | ○ | 1/4 |
| C-34 | 価格訴求の方向の食い違い（p31 と p32） | | | | ○ | 1/4 |

集計: 4/4 が 23 cluster、3/4 が 3、2/4 が 2、1/4 が 6（全 34 cluster）。

### 4.3 Status が変動した cluster（4/4 の 23 cluster のうち）

| Cluster | 01B | S1 | S2 | S3 |
|---|---|---|---|---|
| C-01 | PARTIALLY | UNTRACEABLE | UNTRACEABLE | PARTIALLY |
| C-02 | UNTRACEABLE | PARTIALLY | PARTIALLY | PARTIALLY |
| C-06 | UNTRACEABLE | PARTIALLY | PARTIALLY | PARTIALLY |
| C-07 | UNTRACEABLE | PARTIALLY | UNTRACEABLE | UNTRACEABLE |
| C-11 | PARTIALLY | UNTRACEABLE | UNTRACEABLE | UNTRACEABLE |
| C-13 | UNTRACEABLE | UNTRACEABLE | PARTIALLY | UNTRACEABLE |
| C-17 | UNTRACEABLE | PARTIALLY | PARTIALLY | UNTRACEABLE |
| C-20 | PARTIALLY | PARTIALLY | UNKNOWN | PARTIALLY |
| C-21 | PARTIALLY（他の所見とまとめて） | UNTRACEABLE | PARTIALLY | UNTRACEABLE |
| C-22 | PARTIALLY（他の所見とまとめて） | UNKNOWN | UNKNOWN | UNKNOWN |
| C-23 | UNTRACEABLE | PARTIALLY | PARTIALLY | PARTIALLY |

Status が 4 Run で同じだった cluster（12）: C-03, C-04, C-05, C-08, C-09, C-10, C-12, C-14, C-15, C-16, C-18, C-19。変動したのは上の 11 cluster。C-25（3/4）は PARTIALLY / TRACEABLE / – / TRACEABLE。

観察: Warrant の欠落を扱う cluster（C-02, C-06, C-23）では、01B が UNTRACEABLE、Skill の 3 Run が PARTIALLY TRACEABLE とした。PARTIALLY と UNTRACEABLE の境界は、Run ごと・指示の形ごとに揺れる。

### 4.4 Finding Type が変動した cluster

| Cluster | 使われた Type |
|---|---|
| C-01 | VISUAL_CLAIM（01B）/ OTHER（S1〜S3） |
| C-05 | NARRATIVE（01B）/ FRAMING（S1〜S3） |
| C-06 | AMPLIFICATION / COMMITMENT_ESCALATION / INFERENCE_GAP / INFERENCE_GAP |
| C-09 | COMMITMENT_ESCALATION（01B）/ AMPLIFICATION（S1〜S3） |
| C-10 | INFERENCE_GAP / COMPRESSION / INFERENCE_GAP / INFERENCE_GAP |
| C-13 | SELECTION / AMPLIFICATION / SELECTION / AMPLIFICATION |
| C-15 | TITLE_BODY_GAP（3 Run）/ FRAMING（S3） |
| C-16 | EVIDENCE_INTERPRETATION_BLUR（01B）/ CAUSAL_IMPLICATION（S1〜S3） |
| C-17 | COMMITMENT_ESCALATION（01B）/ AMPLIFICATION（S1〜S3） |
| C-23 | COMMITMENT_ESCALATION（01B）/ AMPLIFICATION（S1〜S3） |

Type が 4 Run で同じだった cluster: C-02, C-04, C-07, C-08, C-14, C-18, C-19, C-20 など。

### 4.5 粒度だけが異なる cluster

| Cluster | 違い |
|---|---|
| C-03 | 01B・S1 は 1 件。S2・S3 は「出典・棒の高さ」と「シナリオの圧縮」の 2 件に分けた |
| C-04 | S3 は「見出しとグラフのずれ」と「確信を落とした Selection」の 2 件に分けた |
| C-10 | S2・S3 は「年額の一括計上」を独立した Finding にした |
| C-11 | S1 は「目盛りの無い比較」と「費用範囲の差」の 2 件。S2・S3 は前者だけを扱った |
| C-12 | 01B は事例の根拠欠落と引用の扱いを分けた。S2・S3 は 1 件にまとめた |
| C-21, C-22, C-29 | 01B は 1 件（F-24）にまとめ、Skill の 3 Run は C-21 と C-22 を分けた |

### 4.6 内容そのものが異なる cluster

| Cluster | 内容の差 |
|---|---|
| C-13 | 「成約率の分母が事前に絞られている可能性」は 01B と S2 だけが指摘した（S1・S3 は強調表現として扱った） |
| C-11 | 「月額費用にアカウント利用料が含まれない」は 01B と S1 だけが指摘した |
| C-24 | 棒の高さの見え方は目視による推定（3 Run とも INFERRED または UNKNOWN と明記） |

---

## 5. 個別の確認

### 5.1 F-26（Run 01B でのみ検出された「雛形の種類の不一致」）

C-27。S2 で再び出現した（2/4）。S1・S3 では出現していない。

### 5.2 Skill Run S1 でのみ検出された 4 件

| S1 の Finding | Cluster | S2 | S3 | 出現 |
|---|---|---|---|---|
| p7 棒の高さの見え方 | C-24 | ○ | ○ | 3/4 |
| 「専門知識不要」と提供形態 | C-31 | | | 1/4 |
| 事例の見出し「未経験」と Before 欄 | C-30 | | | 1/4 |
| 技術サポートの範囲の記述 | C-32 | | 関連あり（S3 は「すべて本部が対応」の範囲が示されていない、という Amplification として扱った） | 1/4（関連 1） |

---

## 6. 所見

- 4 Run に共通する中核: 34 cluster のうち 23 cluster が 4 Run すべてに現れた。Report 構造、Mode 判定、禁止事項の遵守は 4 Run で一致した
- 実行ごとのばらつき: Finding 数（26〜31）、Status の PARTIALLY と UNTRACEABLE の境界、Finding Type の選び方、Finding のまとめ方・分け方は Run ごとに変わる。Skill の 3 Run の間でも同じ種類の変動がある
- Skill と既存 Prompt の差: Skill の 3 Run はそろって Document Class を C（主）とし、Warrant の欠落を扱う cluster の一部を PARTIALLY TRACEABLE とした。01B は A（主）で、同じ cluster を UNTRACEABLE とした。Skill の指示の形による差の可能性があるが、01B は 1 回だけの実行なので、既存 Prompt 側の実行ごとのばらつきとは区別できていない
- 1 Run だけの cluster（6 件）は、すべて成果物の中の記述の食い違いや前提の不一致を扱うもので、どの Run も成果物全体を網羅的に照合してはいないことを示す
- これらは Run Variance / Compatibility Delta として記録する（SC-3: HOLD）。正解・不正解は判定していない。Skill の調整（Finding の追加、Prompt の強化、Status ルールの変更）はしていない

---

## 7. Known Limitations

- 4 Run は同じモデル（Claude Opus 5.5）で実行した。他のモデル・他の AI での挙動は確認していない
- 既存 Prompt の実行は 1 回だけで、Prompt 側のばらつきは測っていない
- cluster のまとめ方は主セッション（AI）が行ったもので、Human の確認を経ていない
- Runtime Test は架空の短い文書 1 件で行った。長い文書・画像を含む資料でのインストール版の挙動は、Variance Test（subagent に Skill を読ませる方式）でのみ確認している
- 自然言語での自動選択は、「Meaning Audit」という語を含む依頼で確認した。「意味の監査」など他の言い方は試していない
- Skill は installable implementation であり、完全な再現性を持つ監査エンジンではない

---

## 8. Human Review Required

| # | 確認すべき問い | Human Decision |
|---|---|---|
| RV-1 | 4/4 の 23 cluster を「Workflow v1.0 で安定して見える Meaning Shift」として扱ってよいか | |
| RV-2 | Status の揺れ（4/4 の 23 cluster のうち 11 cluster）を、FP-003・FP-006 と同じ論点として扱うか | |
| RV-3 | Skill の 3 Run がそろって Class C（主）とした点を、Skill による差として調べるか（既存 Prompt の追加実行が必要） | |
| RV-4 | cluster のまとめ方（34 cluster）は妥当か | |
| RV-5 | Skill を Public v1.0 相当の installable implementation として案内してよいか | |
