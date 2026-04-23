# 第7章 説明可能性・説明責任設計

## 7.1 ML モデルの説明可能性（SHAP）

```python
import shap
from sklearn.ensemble import GradientBoostingClassifier

model = GradientBoostingClassifier().fit(X_train, y_train)
explainer = shap.TreeExplainer(model)
shap_values = explainer.shap_values(X_test)

def explain_prediction(idx: int) -> dict:
    sv = shap_values[idx]
    contributions = {
        feature: float(sv[i])
        for i, feature in enumerate(feature_names)
    }
    top_factors = sorted(contributions.items(),
                         key=lambda x: abs(x[1]), reverse=True)[:5]
    return {
        "prediction": float(model.predict_proba([X_test[idx]])[0][1]),
        "base_value": float(explainer.expected_value),
        "top_factors": top_factors
    }
```

## 7.2 LLM/RAG の説明可能性

LLMは内部構造の解釈が困難なため、「回答内容の根拠」で代替する。

| 技法 | 実装 | 出力例 |
|---|---|---|
| **RAG 根拠文書提示** | 参照ドキュメントID・タイトル・ページを回答に付与 | 「参照: セキュリティポリシー v2.1, p.12」 |
| **類似度スコア開示** | 取得チャンクの cosine similarity を表示 | 「関連度: 0.89」 |
| **情報なし判断** | トップスコア < 0.6 なら「情報なし」と明示 | 「社内ナレッジに該当情報がありません」 |
| **CoT ログ** | 思考プロセスを監査ログに記録 | 設計およびデバッグ目的 |

## 7.3 モデルカードテンプレート

```yaml
model_card:
  model_name: gpt-4o-2024-11-20
  deployment_name: prod-gpt4o-acme
  purpose: 社内ナレッジRAGアシスタント
  owner: AIエンジニアリングチーム
  risk_level: medium
  limitations:
    - 2026-02以降の情報は不完全
    - 日本語の専門用語はハルシネーションリスクあり
  monitoring_kpis:
    hallucination_rate_target: "< 5%"
    pii_leak_rate_target: "0%"
    content_filter_block_rate_alert: "> 2%"
  last_red_team: 2026-01-15
  review_schedule: quarterly
```

## 7.4 EU AI Act リスク分類と説明責任

| リスク分類 | 対象用途 | 説明責任要件 |
|---|---|---|
| **許容不可（禁止）** | 社会スコアリング・潜在意識操作 | 完全禁止 |
| **高リスク** | 採用・医療・金融審査 | 人間の最終判断必須・技術文書・内部監査 |
| **限定リスク** | チャットボット | AIであることをユーザーに開示 |
| **最小リスク** | 一般的業務システム | 自主規制対応 |
