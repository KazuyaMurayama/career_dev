# 第6章 監査ログ設計

## 6.1 LLM 固有の監査ログスキーマ

```json
{
  "request_id": "uuid-v4",
  "timestamp_utc": "2026-04-20T10:23:45.123Z",
  "user": {
    "user_id": "u_12345",
    "tenant_id": "tenant_acme",
    "role": "EndUser"
  },
  "request": {
    "input_hash": "sha256:abc123...",
    "input_token_count": 234,
    "input_pii_detected": false,
    "input_blocked": false
  },
  "model": {
    "deployment_name": "gpt-4o-2024-11-20",
    "temperature": 0.0
  },
  "rag": {
    "retrieved_doc_ids": ["doc_001", "doc_002"],
    "retrieval_filter_applied": {"tenant_id": "tenant_acme"},
    "top_k": 5
  },
  "response": {
    "output_hash": "sha256:def456...",
    "output_token_count": 312,
    "output_pii_detected": false,
    "content_filter_result": {"hate": "safe", "violence": "safe"},
    "hallucination_score": 0.87,
    "latency_ms": 1423
  },
  "outcome": {
    "delivered_to_user": true,
    "filter_blocked": false
  }
}
```

## 6.2 保存要件・WORM設定

| 項目 | 要件 |
|---|---|
| 保存期限 | 最伜1年（金融業では7年） |
| 改ざん防止 | Azure Blob Storage の Immutability Policy（WORM）を有効化 |
| 暗号化 | ログに個人情報を含めない。含む場合はハッシュ化 |
| アクセス制御 | AuditViewer ロールのみ閲覧可能。安易に削除できない構成 |

## 6.3 リアルタイムアラート閖値

| アラート条件 | 閖値 | 重大度 | 対応 |
|---|---|---|---|
| PII 出力検出 | 1件/分 | Critical | 即時サービス停止 |
| コンテンツフィルタブロック | 10件/分 | High | セキュリティチームへ通知 |
| ハルシネーションスコア < 0.7 | 平均の20%超過 | Medium | デプロイバージョン確認 |
| レートリミット超過 | ユーザー当たり100件/時間 | Medium | 該当ユーザーを一時封鎖 |
| コスト異常 | 日次予算の150% | Medium | コストアラート・DoS調査 |

## 6.4 Azure 実装構成

```
Azure OpenAI
  ↓ Diagnostic Settings
Azure Monitor
  ↓ Log Analytics Workspace
Microsoft Sentinel  ←  アラートルール
  ↓
セキュリティチームノティフィケーション (Teams/メール)
```
