# dags/

> Airflow DAG 定義。

## 結構

```
dags/
├── daily_pipeline.py        # 每日 6am ingest + transform
├── hourly_classifier.py     # 每小時跑 LLM 分類
└── weekly_report.py         # 每週日寄 email 報告
```

## DAG 撰寫慣例

1. **import src 的函式**，DAG 只負責「順序 + 排程」，邏輯不在 DAG 裡
2. **每個 task 都加 retry**（業界要求）
3. **失敗推送 LINE / Slack**
4. **task 名稱 snake_case + verb**：`fetch_articles` 不是 `articles`

## 範例

```python
from datetime import datetime, timedelta
from airflow import DAG
from airflow.operators.python import PythonOperator

from src.ingest.pipeline import run_daily_ingest
from src.analytics.classifier import classify_batch
from src.serve.notifications.line_bot import notify_failure

default_args = {
    "owner": "team",
    "retries": 3,
    "retry_delay": timedelta(minutes=5),
    "on_failure_callback": notify_failure,
}

with DAG(
    "daily_pipeline",
    default_args=default_args,
    schedule="0 6 * * *",       # 每天 6am
    start_date=datetime(2026, 4, 1),
    catchup=False,
    tags=["production"],
) as dag:

    ingest = PythonOperator(
        task_id="fetch_articles",
        python_callable=run_daily_ingest,
    )

    classify = PythonOperator(
        task_id="classify_batch",
        python_callable=classify_batch,
    )

    ingest >> classify
```

## 測試 DAG

```bash
# 本地測 import + syntax
python dags/daily_pipeline.py

# 在 Airflow UI 手動觸發 + 看 log
docker compose up airflow
# 開 http://localhost:8080
```
