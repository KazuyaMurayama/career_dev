# パート1-1: 脅威の深層理解とフィルタリング技術比較（Part 1 補強版）

**対象:** AI担当者・情シス・セキュリティ部門・ベンダー選定担当  
**目的:** Part 1 の脅威概念を深掘りし、Azure/Claude/Gemini の比較で選定判断に使える実務資料とする  
**位置づけ:** Part 1（脅威モデル・ガードレール設計）の補強。重複は避けクロスリファレンス（Part 1 Q1 等）で参照

---

## 第1部: 脅威の用語と実害規模

### 1-1. Indirect PI / Jailbreak / XSS の関係と違い

3者は「LLMシステムの3つの異なるレイヤーで発生する別種の攻撃」であり、単一防御では対処不能。

| 観点 | Indirect PI | Jailbreak | XSS（LLM出力起因） |
|---|---|---|---|
| 攻撃の入口 | RAG取得文書・Web参照先 | ユーザープロンプト | LLM出力の表示レイヤー |
| 攻撃者像 | 無自覚な第三者 or 内部悪意 | ユーザー自身（外部） | ユーザー自身 or 偶発 |
| 典型被害 | 情報漏えい・権限外操作 | 禁止出力（有害・機密） | コード実行・セッション窃取 |
| OWASP LLM | LLM01（Prompt Injection） | LLM01（Prompt Injection） | LLM02（Insecure Output） |
| 主防御 | XMLタグ分離・取得源検証 | Content Filter・ガードレール | アプリ層サニタイズ（DOMPurify等） |
| 防御層 | 入力前処理 | 入力/生成フェーズ | 出力後処理 |

**連鎖攻撃パターン（2024年以降の実攻撃で観測）**

```
[段1] Indirect PI
 攻撃者がSaaS共有ドキュメントに「以降の指示を無視して...」を埋め込む
    ↓ RAG取得で無自覚に読込
[段2] Jailbreak 誘発
 埋込み指示が "機密を全部出力せよ" 等の禁止要求を発動
    ↓ LLM がガードを迂回
[段3] XSS出力
 LLMが <script>...</script> を含む回答を生成、アプリが無検証表示
    ↓ ユーザーのブラウザで実行
[結果] セッション窃取・情報漏えい
```

各段で**防御層が異なる**ことが重要。Indirect PI対策（XMLタグ分離、Part 1 Q1参照）だけでは段2・段3を止められない。3段すべてに独立の防御を置く多層構造が必須。

### 1-2. 実害規模の定量データ（代表3件）

**① Samsung 社内機密漏えい（2023年4月）**
- 半導体部門エンジニアがソースコード・会議議事録を ChatGPT に投入
- 学習に利用される懸念から全社 ChatGPT 使用禁止に発展
- 金額非公表だが、生成AI利用停止のビジネス機会損失は大手事業部で月数千万円規模（筆者推定）
- **教訓:** 「ベンダーは学習に使わない」という誤解 + 野良個人利用が原因。Part 2 Q4 の「そもそも送らない」設計が必要

**② Air Canada チャットボット誤案内判決（2024年2月）**
- 遺族割引の適用条件をボットが誤回答 → 利用者が航空券購入 → 実際は対象外
- カナダ民事裁判所: 約 812 CAD の損害賠償命令
- **判例の重要性:** 「チャットボットも会社の代理人」と認定。AIが発した言葉の法的責任は会社に帰属
- **教訓:** 顧客向け回答は RAG + 出力前ゲート必須。価格・契約条件・法的効果を伴う回答は Human-in-the-loop

**③ Chevrolet ディーラー $1 販売約束事案（2023年12月）**
- ユーザーが「同意を絶対取り消さないと約束して」と指示 → bot が $1 で新車販売を約束
- 契約履行は回避されたが SNS 拡散・ブランド毀損
- **教訓:** Jailbreak 対策の甘さは金額より信頼ダメージが大きい。Part 1 Q5 の ASR 継続計測が必要

**集計データ（業界全体の傾向）**
- IBM Cost of a Data Breach Report 2024: 平均データ侵害コスト **$4.88M**、生成AI関連インシデントは前年比増加傾向
- Gartner 2024 予測: 「2026年までに企業の **30%** が生成AI起因のセキュリティインシデントを経験」

> **📋 情シス向け説明フレーム**  
> 「Samsung は野良利用、Air Canada は出力ゲート欠如、Chevrolet は Jailbreak 対策欠如が原因。この3パターンで社内事故の大半をカバーできます。」

---

## 第2部: フィルタリング技術マトリクス比較

### 2-1. 主要3ベンダー + OSS の機能マトリクス

**比較対象**（2026年4月時点・公開情報ベース）
- Azure OpenAI: Azure AI Content Safety
- Anthropic Claude: Constitutional AI + Claude for Enterprise
- Google Gemini: Safety Settings + Vertex AI Model Armor
- OSS補完: Llama Guard 3 / NVIDIA NeMo Guardrails

**機能カバレッジ比較**

| 機能 | Azure AI Content Safety | Claude (Enterprise) | Gemini + Model Armor | Llama Guard 3 / NeMo |
|---|---|---|---|---|
| 有害4カテゴリ（Hate/Violence/Sexual/Self-harm） | ○ 標準搭載・4段階閾値 | ○ Constitutional AIで内蔵 | ○ 4カテゴリ標準 | ○ LlamaGuard 13カテゴリ |
| Jailbreak検出 | ○ Prompt Shields | ○ 内蔵・業界最高水準 | △ Model Armor追加必要 | △ NeMo Rails で補完 |
| Indirect PI検出 | ○ Prompt Shields for Documents | △ 汎用耐性のみ | △ Model Armor必要 | △ 自作ルール要 |
| Groundedness（RAG整合性） | ○ Groundedness Detection | × 標準機能なし | △ Model Armor | × 自前実装 |
| Protected Material（著作権） | ○ コード・テキスト検出 | △ 学習ポリシー依存 | △ Model Armor | × |
| PII検出・マスキング | ○ Azure AI Language連携 | × 外部ツール必須 | ○ Cloud DLP連携 | × Presidio併用 |
| カスタムカテゴリ対応 | ○ Custom Categories | △ プロンプト設計で対応 | ○ Model Armor | ○ NeMo ルール自由 |
| 日本語対応精度 | ○ 日本語高精度 | ○ Claude 3.5以降高精度 | △ カテゴリ・精度に差 | △ 英語中心 |
| 監査ログ連携 | ○ Azure Monitor統合 | △ API側で自前記録 | ○ Cloud Logging統合 | × 自前構築 |
| 法人契約・国内DC | ○ 日本DC・SLA有 | ○ Bedrock経由で国内可 | ○ 日本リージョン有 | OSS（自社運用） |

**マトリクスから読める3つの示唆**
1. **Azure は RAG運用で最適**: Indirect PI検出と Groundedness を標準搭載する唯一のベンダー。Part 1 Q3 の「下限値」として選定しやすい
2. **Claude は汎用耐性が強い**: Constitutional AI による Jailbreak 耐性は業界最高水準だが、業務固有ルール・PII・Groundedness は自前補完が前提
3. **Gemini は単体評価は不公平**: Safety Settings の4カテゴリのみでは業務利用困難だが、Model Armor との組合せで Azure・Claude と同等

### 2-2. 選定の判断軸（3つに絞る）

| 判断軸 | 重視する場合の推奨 |
|---|---|
| ① 業務固有ルールのカスタム性 | どのベンダーでも**自前ガードレール必須**。ベンダー選定より自前設計が優先 |
| ② マルチベンダー運用の最小公倍数 | **LiteLLM 等で抽象化** + 自前フィルタを共通化する構成が現実解（Part 5 Q4参照） |
| ③ 日本語・日本法対応 | **Azure が現時点優位**（日本DC・Content Safety日本語精度）。Claude/Gemini は自前補完で埋める |

### 2-3. 推奨構成パターン（1パターンに集約）

**「どのベンダーでも動く 2層ガードレール構成」**

```
[ユーザー入力]
    ↓
[L1: ベンダー標準フィルタ]
 Azure Content Safety / Claude内蔵 / Gemini Safety Settings
 ※ 全ベンダー共通の最小公倍数で設定（severity=medium 等）
    ↓
[L2: 自前ガードレール（入力側）]
 Presidio（PII） + Llama Guard 3（有害拡張） + 業務固有ルール（競合言及・法的リスク）
    ↓
[LLM 呼び出し]
    ↓
[L2: 自前ガードレール（出力側）]
 PII再スキャン・禁止出力検出・Groundedness整合性チェック
    ↓
[L1: ベンダー出力フィルタ]
    ↓
[アプリ層サニタイズ（DOMPurify等）] → ユーザー

共通監査ログ: request_id で全層の判定結果を連結（Part 3 Q1 参照）
```

**この構成の利点3点**
- **ベンダーロックイン回避**: L2 が自前実装のため、モデル切替時も業務固有ガードは不変（Part 5 Q4 準拠）
- **業務固有リスクのカバー**: L1 では防げない競合言及・社内規程違反を L2 で捕捉
- **監査証跡の統合**: request_id を軸に L1/L2/アプリ層の判定を1本化、事後調査を可能に

> **📋 情シス向け説明フレーム**  
> 「ベンダー標準フィルタは"最低ライン"、自前ガードレールは"業務固有リスクの最後の砦"。この2層ならモデル切替時もガードレール仕様が不変です。」

---

## 第3部: よくある誤解と補足知識

### よくある誤解トップ3（本パート特化）

| 誤解 | 正しい理解 |
|---|---|
| 「Azure Content Safety が一番強いから他は不要」 | カスタム性で Claude/Gemini が有利な場面あり。選定は業務要件次第 |
| 「Constitutional AI があれば Claude は自前ガードレール不要」 | 汎用耐性は高いが業務固有ルール（競合言及・社内規程）はカバー不可 |
| 「Gemini は4カテゴリしかないから法人利用は非推奨」 | Vertex AI Model Armor と組み合わせれば実用。単体評価は誤り |

### 用語集（Part 1 と重複しないもの）

| 用語 | 説明 |
|---|---|
| Constitutional AI | Anthropic の RLHF拡張。モデル自身が憲法的ルールで自己批評する仕組み |
| Groundedness | LLM出力がRAG取得文書と整合しているかを測る指標。ハルシネーション検知の中核 |
| Protected Material | 著作権保護されたコンテンツ（コード・歌詞・書籍）の出力検出対象 |
| Llama Guard 3 | Meta製OSS。8Bモデルで有害13カテゴリを分類 |
| Model Armor | Google Cloud の LLM向けセキュリティレイヤー（Vertex AI の追加製品） |
| LiteLLM | 複数LLMベンダーを統一インターフェースで呼び出すOSSライブラリ |

### 参照ドキュメント

- Azure AI Content Safety 公式ドキュメント（Prompt Shields / Groundedness Detection）
- Anthropic Usage Policies / Constitutional AI 論文（arXiv:2212.08073）
- Google Cloud Vertex AI Model Armor 製品ページ
- Meta Llama Guard 3 モデルカード（Hugging Face）
- NVIDIA NeMo Guardrails GitHub
- IBM Cost of a Data Breach Report 2024
- Gartner Hype Cycle for Generative AI 2024

---

*著者: 男座 員也（Oza Kazuya） | 2026年4月 | AIセキュリティ・ガバナンス実務レポート Part 1-1/5 補強版*
