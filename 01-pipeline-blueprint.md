# 01 通用資料管線藍圖

> 看完這篇你會獲得一個能用十年的心智模型：所有 DE 專案都長同一個樣子，只是每個 stage 用不同工具。

---

## 一句話總結

**所有資料管線都是 6 個階段：Source → Ingest → Storage → Transform → Serve → Observe。**

你的 8 情境也好，業界 PB 級系統也好，骨架完全一樣。差別只在每階段的選型。

---

## 六階段藍圖

```
┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐
│ Source  │→ │ Ingest  │→ │ Storage │→ │Transform│→ │  Serve  │→ │ Observe │
│ 資料源  │  │ 進料    │  │ 儲存    │  │ 加工    │  │ 服務    │  │ 監控    │
└─────────┘  └─────────┘  └─────────┘  └─────────┘  └─────────┘  └─────────┘
   ↑                                                                  │
   └──────────────── feedback loop（監控發現問題 → 改進 source）─────┘
```

### 1️⃣ Source — 資料從哪來

| 形式 | 範例 | 學期會碰到 |
|---|---|---|
| API（被動拉） | OpenAI / Spotify / 政府開放資料 | ✅ |
| 爬蟲（主動抓） | momo / 104 / 巴哈姆特 | ✅ |
| 檔案下載 | Kaggle CSV / 實價登錄 zip | ✅ |
| 資料庫匯出 | 企業 ERP MySQL dump | 期末才會碰 |
| Streaming | Kafka topic / Pub/Sub | 進階 |

**選型原則**：能用 API 別用爬蟲，能用爬蟲別硬刻。

### 2️⃣ Ingest — 怎麼把資料拉進來

| 模式 | 工具 | 何時用 |
|---|---|---|
| 一次性手動 | Python + requests | POC 階段 |
| 排程批次 | Airflow / cron / GitHub Actions | 多數情境 |
| 即時串流 | Kafka / Pub/Sub | 高頻 + 低延遲 |
| 事件觸發 | Webhook + Cloud Function | 整合第三方 |

**陷阱**：學員 90% 用「手動跑」就交作業 → 業界看到就刷掉。**必須上排程**。

### 3️⃣ Storage — 資料放在哪

```
原始層（Raw / Bronze）        → MongoDB / GCS / S3 / 本地 parquet
   ↓
清洗層（Cleaned / Silver）    → MySQL / PostgreSQL
   ↓
分析層（Curated / Gold）      → BigQuery / dbt model
```

**新手最常犯**：只放一張 MySQL table，原始資料直接覆蓋掉 → 出錯了沒救。

**業界原則**：**Raw 永遠保留**，只在 Silver / Gold 層做清洗。

### 4️⃣ Transform — 加工成可用資訊

| 工具 | 適用 |
|---|---|
| pandas | 中小資料（<10 GB）、單機 |
| SQL (BigQuery / Postgres) | 大資料分析 |
| dbt | 維度建模、版本控制的 SQL |
| Spark | 超大資料、分散式 |
| LLM API | 文字理解 / 分類 / 摘要 |

**新手最常犯**：把所有邏輯塞進一支 1000 行的 notebook。
**業界做法**：拆成 staging → intermediate → mart 三層，每層職責清楚。

### 5️⃣ Serve — 怎麼讓人用到

| 形式 | 工具 | 何時用 |
|---|---|---|
| Dashboard | Streamlit / Tableau / Looker | 內部視覺化 |
| API | FastAPI / Flask | 給其他系統呼叫 |
| Chat Bot | LINE Bot / Discord Bot | 一般用戶 |
| 報告 | Notebook + PDF export | 一次性分析 |
| Notification | Email / Slack / LINE 推播 | 警示型 |

**選型原則**：跟著「使用者怎麼用」走，不是跟著「我會什麼」走。

### 6️⃣ Observe — 出問題你知道嗎？

| 監控項目 | 工具 |
|---|---|
| Pipeline 跑沒跑 | Airflow UI / Sentry |
| 資料品質 | dbt tests / Great Expectations |
| API 健康 | Uptime Robot / Cloudflare |
| Cost | GCP Billing / AWS Cost Explorer |
| Alert | Email / Slack / LINE notify |

**新手 99% 跳過這一步** → 就是這一步把作品集從 🟡 升到 ✅。

---

## 怎麼套用到 8 情境

| # | 情境 | Source | Storage | Transform | Serve |
|---|---|---|---|---|---|
| 1 | 餐飲 POS | Kaggle / API | MySQL | pandas | Streamlit |
| 2 | 電商比價 | 爬蟲 (momo/PChome) | MySQL | Airflow + SQL | FastAPI |
| 3 | 數位金融 | CFPB API | MongoDB | LLM 分類 | Streamlit |
| 4 | 音樂串流 | Spotify API | MongoDB | SQL + pandas | Streamlit |
| 5 | 叫車交通 | NYC TLC | BigQuery | Airflow 15 min | FastAPI |
| 6 | 求職媒合 | 104 爬蟲 | MongoDB | pandas | Streamlit |
| 7 | 新聞輿情 | RSS / NewsAPI | MongoDB | LLM | Streamlit + LINE |
| 8 | 房地產 | data.gov.tw | MySQL | pandas | Streamlit 地圖 |

每個情境的細節展開請見 `scenarios/*.md`。

---

## 工具選型 3 條決策樹

### 樹 1：資料規模

```
你的資料每天進多少？
├ <1 GB        → MySQL / MongoDB 就夠
├ 1-100 GB     → BigQuery / PostgreSQL
└ >100 GB      → BigQuery / Snowflake / Spark
```

### 樹 2：更新頻率

```
資料多久要新一次？
├ 每天 / 每週   → cron / GitHub Actions
├ 每小時 / 15min→ Airflow
└ 即時          → Kafka / Pub/Sub
```

### 樹 3：使用者

```
誰在用你的結果？
├ 工程師 / 自己   → 寫 notebook 或 SQL 就好
├ 非技術同事     → Streamlit / Tableau
├ 一般用戶       → LINE Bot / 網頁
└ 其他系統       → FastAPI
```

---

## 三個常見誤區

1. **「我要學最潮的技術」** → 沒人在乎你用 Snowflake 還是 MySQL，業界在乎你解了什麼問題
2. **「我要做完美再 demo」** → 完美等於拖延，先做出 v0 跑完整條 pipeline，再回來優化每段
3. **「我自己做就好」** → 作品集如果沒 PR 紀錄，業界看不出你會不會協作

---

下一步：[02 小組專案 10 階段流程 →](02-team-process.md)
