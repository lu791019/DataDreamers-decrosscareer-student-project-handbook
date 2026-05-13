# src/ — 程式碼根目錄

按職責拆 4 個模組，每個模組對應 1 個小組成員（主擔）。

## 結構

```
src/
├── ingest/         # Owner: @ingest_owner
│   ├── __init__.py
│   ├── schemas.py        # pydantic models 給 raw 資料用
│   ├── {source1}.py      # 各個來源的 client
│   ├── {source2}.py
│   └── pipeline.py       # 進料邏輯（給 Airflow 呼叫）
│
├── pipeline/       # Owner: @pipeline_owner
│   ├── __init__.py
│   ├── airflow/          # DAGs
│   │   └── daily_dag.py
│   └── transforms/       # 共用 transformation 函式
│
├── analytics/      # Owner: @analytics_owner
│   ├── __init__.py
│   ├── data_loader.py    # 從 storage 讀資料
│   ├── classifier.py     # LLM / model 分類
│   ├── recommender.py    # 推薦演算法
│   └── trend.py          # 趨勢分析
│
└── serve/          # Owner: @product_owner
    ├── __init__.py
    ├── dashboard.py       # Streamlit
    ├── api.py             # FastAPI
    └── notifications/    # LINE Bot / Email
        └── line_bot.py
```

## 命名約定

- snake_case
- 函式：動詞開頭（`fetch_articles` 不是 `articles`）
- 私有：`_underscore_prefix`
- 常數：`UPPER_CASE`
- type hints：必要
- docstring：對外函式必有

## 測試

對應到 `tests/`：

```
tests/
├── unit/
│   ├── ingest/
│   ├── analytics/
│   └── serve/
└── integration/
    └── e2e_test.py
```

## 進入 / 退出點

```python
# Airflow DAG 呼叫
from src.ingest.pipeline import run_daily_ingest
from src.analytics.classifier import classify_batch

# Streamlit 入口
# streamlit run src/serve/dashboard.py

# FastAPI 入口
# uvicorn src.serve.api:app
```
