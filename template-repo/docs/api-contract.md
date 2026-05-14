# 模組間 API 契約

> 4 個模組怎麼互動 — 寫清楚這份，整合時就不會吵架。

---

## 原則

1. **每個介面都要有契約** — 不存在「兩個模組私下講好」
2. **schema 用程式驗證** — pydantic / jsonschema，不要靠註解
3. **不向後兼容的變更要先開 issue 討論** — 標 `[schema-change]`

---

## 1. Ingest → Storage

### Ingest 寫進 MongoDB 的格式

```python
# src/ingest/schemas.py
from pydantic import BaseModel
from datetime import datetime

class RawArticle(BaseModel):
    source: str           # "newsapi" / "rss" / "ptt"
    source_id: str        # 原始 ID
    url: str
    title: str
    content: str
    published_at: datetime
    fetched_at: datetime
    metadata: dict = {}
```

### MongoDB Collection
- DB: `project_db`
- Collection: `raw_articles`
- Index: `(source, source_id)` unique；`fetched_at`

---

## 2. Storage → Process

### Process 從 Storage 讀的查詢

```python
# src/analytics/data_loader.py
def load_unprocessed_articles(since: datetime) -> pd.DataFrame:
    """讀取尚未分類的文章"""
    ...

def save_classifications(items: list[ClassifiedArticle]):
    """寫回分類結果到 classified_articles collection"""
    ...
```

### Schema
```python
class ClassifiedArticle(BaseModel):
    article_id: str             # 對應 raw.source_id
    category: Literal["FEE", "CARD", "SYSTEM", "OTHER"]
    sentiment: int              # 1-5
    confidence: float           # 0-1
    classifier_version: str     # e.g. "v3"
    classified_at: datetime
```

---

## 3. Process → Serve

### Serve（Streamlit / API）讀什麼

```python
# src/serve/queries.py
def get_trend(category: str, days: int = 30) -> pd.DataFrame:
    """過去 N 天某類別的趨勢"""
    ...

def get_alerts(threshold: float = 0.8) -> list[Alert]:
    """目前活躍警示"""
    ...
```

### FastAPI Endpoint

```yaml
# OpenAPI 摘要
GET /api/v1/trend?category=FEE&days=7
  Response: { dates: [], counts: [], avg_sentiment: [] }

GET /api/v1/alerts?level=critical
  Response: [{ id, type, message, triggered_at }]

POST /api/v1/feedback
  Body: { article_id, user_id, correct_category }
  Response: { ok: bool }
```

---

## 4. 共用 Observability 契約

任何模組失敗都要：

```python
import sentry_sdk

try:
    do_work()
except Exception as e:
    sentry_sdk.capture_exception(e)
    notify_line(f"[{module_name}] Failed: {e}")
    raise
```

---

## Schema 變更流程

1. 開 issue 標 `[schema-change]`
2. 至少 1 個其他模組 owner approve
3. 同時改：上游寫入、下游讀取、migration script
4. 合 PR 後在 standup 通知所有人

---

## Versioning

| 介面 | 目前版本 | 變更紀錄 |
|---|---|---|
| MongoDB raw_articles | v1 | 初版 |
| classified_articles | v2 | 加 confidence 欄位（PR #34） |
| FastAPI | v1 | 初版 |
