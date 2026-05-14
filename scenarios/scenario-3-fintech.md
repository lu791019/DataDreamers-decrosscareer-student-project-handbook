# 情境 3：數位金融客訴效率 + 滿意度

> **一句話**：給銀行客服主管一個「今天哪類客訴在爆、誰要負責、是否要 escalate」的智能儀表板。

---

## 為誰解什麼

- **目標用戶**：純網銀客服主管 / 傳統銀行數位部
- **痛點**：客訴量大、人工分類慢、SLA 容易超過、滿意度趨勢看不出
- **量化目標**：客訴分類自動化 95% 精度；SLA 違反提早 30 分鐘預警

---

## 業界對標

→ 詳見 [05 痛點地圖 - 情境 3](../05-pain-points-industry-map.md#情境-3數位金融客訴效率--滿意度)

**過往學長姐 demo**：
- [07 反詐騙 LINE Bot（TIR104）](https://youtu.be/d0_EgIgMjOU)
- [06 打造自己的 ETF（TIR103）](https://youtu.be/pZZzNfOSdHA)

---

## 6 階段藍圖具體化

```
Source                  Ingest             Storage         Transform        Serve            Observe
─────                   ──────             ───────         ─────────        ─────            ───────
CFPB Complaint API     requests + cron    MongoDB          LLM API           Streamlit        Sentry
PTT 銀行版              （每日 / 每小時）  (raw_complaints  + pandas          + LINE推播       + LLM cost 
模擬客服紀錄             Airflow           / classified)    (分類+情緒)       (主管警示)        watcher
```

---

## 資料源細節

| 資料源 | 取得方式 | 規模 | 用來做 |
|---|---|---|---|
| [CFPB Complaint Database](https://www.consumerfinance.gov/data-research/consumer-complaints/) | 開放 API | 上百萬筆英文客訴 | 訓練分類模型 |
| [Kaggle Bank Customer Complaints](https://www.kaggle.com/datasets) | 下載 CSV | ~10 萬筆 | 補充 |
| PTT 銀行版（模擬） | 爬蟲 | 每月 ~500 筆 | 中文場景 |

> 中文資料可以用 LLM 翻譯 CFPB 補強

---

## 10 階段執行重點

### ① 啟動
- 選題理由：FinTech 是熱門賽道、LLM 應用真實價值高
- 注意：個資要去識別化（即使是公開資料也好習慣）

### ② Discovery
- Persona 範例：純網銀客服主管 Linda（15 人團隊、每天 200 筆客訴）
- 痛點：(1) 分類靠人工眼掃 (2) SLA 4 小時、超過會被申訴 (3) 月報老闆要看「熱點變化」

### ③ 設計
- 分類體系：手續費 / 卡片問題 / 系統錯誤 / 帳號異常 / 客服態度 / 其他
- 情緒分數：1-5 + 紅黃綠燈
- 三層 schema：raw / classified / aggregated

### ④ 分工
| 角色 | 任務 |
|---|---|
| Ingest | CFPB API + PTT 爬蟲 + 去識別化 |
| Pipeline | Airflow 每小時 + LLM batch + cost control |
| Analytics | LLM 分類 prompt 設計 + 評估 + 警示邏輯 |
| Product | Streamlit dashboard + LINE Bot 推播 |

### ⑤ 環境
- `.env` 一定要 gitignore（OpenAI key）
- 建議用 OpenAI batch API 省成本

### ⑥ 衝刺

**Sprint 1（W10-W12）**：
- 1000 筆 CFPB → MongoDB → LLM 跑分類
- 看分類準確率（人工抽 30 筆對）

**Sprint 2（W13-W15）**：
- 整套 pipeline 自動跑
- 情緒分析 + SLA 警示邏輯
- Streamlit dashboard 雛形

**Sprint 3（W16-W18）**：
- LINE Bot 推播
- 加 cost watcher（每天 LLM 花多少）
- 主管視圖 / 客服視圖切換

### ⑦ 整合
- 端到端：新客訴 → 5 分鐘內分類 → SLA 預警 → LINE 推播
- 整合測試：餵 50 筆已標註資料，看自動結果跟人工差幾筆

### ⑧ 上線
- Streamlit Cloud + LINE Bot webhook 在 Cloud Run
- Airflow + MongoDB 在 GCP

### ⑨ Demo
強調「**真實業界場景**」：
1. 開 dashboard 展示「過去 7 天熱點」
2. 模擬一筆新客訴進來，LINE 即時推播
3. 講 cost：「我們每天 LLM 花 30 元、人工要花 1 萬」

### ⑩ 復盤
重點反思：LLM prompt 怎麼迭代、cost 怎麼控

---

## 範例 prompt 設計（LLM 分類）

```python
SYSTEM = """你是銀行客訴分類專家。
請將客訴分到下列 6 類之一：
- 手續費爭議 (FEE)
- 卡片問題 (CARD)
- 系統錯誤 (SYSTEM)
- 帳號異常 (ACCOUNT)
- 客服態度 (SERVICE)
- 其他 (OTHER)

並評估情緒分數 1-5（1 極負面、5 中性偏正）。

只回傳 JSON：{"category": "FEE", "sentiment": 2, "reason": "..."}"""

USER = "客訴內容：{complaint_text}"
```

> 業界級做法：給 5-shot examples + 用 batch API 降 50% 成本

---

## 範例 commit log

```
* feat: CFPB API ingest with pagination (#3)
* feat: MongoDB schema with raw + classified collection (#5)
* feat: LLM classifier with 6 categories + sentiment (#8)
* test: classifier accuracy eval on 100 labeled samples - 92% (#10)
* feat: SLA breach detection with 30min advance warning (#13)
* feat: LINE Bot push notification on critical complaints (#16)
* feat: streamlit dashboard with manager/agent views (#19)
* perf: switch to OpenAI batch API - 50% cost reduction (#22)
* docs: prompt engineering decisions (ADR-003) (#24)
```

---

## 進階挑戰

- [ ] **Vector DB + RAG**：客服輸入新客訴 → 找出歷史類似案例 → 建議回應稿
- [ ] **Kafka streaming**：客訴從 producer 進來，5 秒內分類完
- [ ] **Multi-language**：自動偵測語言 + 翻譯 + 分類
- [ ] **Drift monitoring**：分類分佈變動超過閾值 alert

---

## 雷區

| 雷 | 為什麼 |
|---|---|
| 每筆都用 GPT-4 | 1 萬筆破 5000 元 |
| 沒去識別化 | 個資法地雷 |
| 分類精度沒評估 | demo 時被問就掛 |
| Prompt 寫在 code 裡 hardcoded | 沒法迭代 |

---

## 重要：個資處理

- 客訴內容**去識別化**：姓名 / 電話 / 卡號 → mask
- 用正則 + LLM 雙重檢查
- 訓練資料和測試資料分開

---

## 完整時程（總 20 週）

| 週 | 階段 | 重點產出 |
|---|---|---|
| W1-W3 | 啟動 | LLM API key + cost budget |
| W2-W4 | Discovery | 分類體系設計 |
| W4-W7 | 設計 + 分工 | prompt engineering plan |
| W10-W12 | Sprint 1 | 1000 筆跑通 + 精度評估 |
| W13-W15 | Sprint 2 | 全自動 pipeline + dashboard |
| W16-W18 | Sprint 3 | LINE Bot + cost control |
| W19 | 整合 + 上線 | end-to-end test + 雲端 |
| W20 | Demo + 復盤 | 強調 LLM 應用商業價值 |

---

← [上個情境：2 電商比價](scenario-2-ecommerce.md) | 下個情境：[4 音樂串流 →](scenario-4-music.md)
