# 資料字典

> 所有資料表 / collection 的欄位定義。新人 onboarding 必讀。

---

## raw_articles（MongoDB collection）

| 欄位 | 型別 | 必填 | 說明 | 範例 |
|---|---|---|---|---|
| `_id` | ObjectId | ✅ | MongoDB 自動產生 | - |
| `source` | string | ✅ | 來源類型 | `"newsapi"` |
| `source_id` | string | ✅ | 來源原始 ID | `"art-12345"` |
| `url` | string | ✅ | 文章 URL | `"https://..."` |
| `title` | string | ✅ | 標題 | `"OpenAI..."` |
| `content` | string | ✅ | 全文 | `"..."` |
| `published_at` | datetime | ✅ | 文章發布時間 | `2026-05-10T10:00:00Z` |
| `fetched_at` | datetime | ✅ | 我們抓的時間 | `2026-05-10T10:05:00Z` |
| `language` | string |  | 語言 | `"zh"` |
| `metadata` | object |  | 來源特定欄位 | `{...}` |

**Index**:
- `(source, source_id)` unique
- `fetched_at` desc
- text index on `title + content`

---

## classified_articles（MongoDB collection）

| 欄位 | 型別 | 必填 | 說明 |
|---|---|---|---|
| `article_id` | string | ✅ | 對應 raw_articles.source_id |
| `category` | enum | ✅ | FEE / CARD / SYSTEM / OTHER |
| `sentiment` | int | ✅ | 1-5（1 極負面、5 正面） |
| `confidence` | float | ✅ | LLM 信心度 0-1 |
| `keywords` | array<string> |  | 抽取的 3-5 關鍵字 |
| `classifier_version` | string | ✅ | e.g. "v3" |
| `classified_at` | datetime | ✅ | 分類時間 |

---

## predictions（MySQL table）

```sql
CREATE TABLE predictions (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    region_code VARCHAR(20) NOT NULL,
    predict_for DATE NOT NULL,
    predicted_value DECIMAL(12, 2),
    confidence_lower DECIMAL(12, 2),
    confidence_upper DECIMAL(12, 2),
    model_version VARCHAR(20) NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE KEY uk_region_date_model (region_code, predict_for, model_version)
);
```

| 欄位 | 說明 |
|---|---|
| `region_code` | 區域代碼（H3 hex / 行政區） |
| `predict_for` | 預測哪一天 |
| `predicted_value` | 預測值 |
| `confidence_lower/upper` | 95% 信心區間 |

---

## ER 關係

```
raw_articles (1) ──── (1) classified_articles  via article_id

raw_articles (N) ──── (1) topics  via topic_id (from clustering)

predictions (independent table)
```

---

## 命名約定

- 表 / collection：snake_case 複數（`raw_articles`、`classified_articles`）
- 欄位：snake_case
- enum 值：UPPER_CASE
- 時間戳：UTC、用 ISO 8601、欄位名 `_at` 結尾
- ID：source_id / region_code 等清楚字尾

---

## Schema 演進策略

新增欄位：optional + default value → 不影響舊資料 → 不算 breaking change
改現有欄位型別 / rename：breaking change → 需要 migration script
刪除欄位：先廢棄 1 個 sprint → 確認沒人用 → 才刪

詳見 [api-contract.md](api-contract.md) 的「Schema 變更流程」
