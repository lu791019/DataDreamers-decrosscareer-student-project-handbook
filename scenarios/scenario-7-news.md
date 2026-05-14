# 情境 7：媒體業新聞輿情即時監測

> **一句話**：給品牌 / 公關公司一個「我的品牌今天有沒有被罵、誰在罵、要不要回應」的智能監控。

---

## 為誰解什麼

- **目標用戶**：品牌行銷經理 / 公關公司 AE / 媒體編輯
- **痛點**：負面輿情爆發後才知道；人工掃文章不可能即時；不知道下一波議題在哪
- **量化目標**：負面議題 1 小時內偵測；分類精度 ≥ 85%；月省人工監控時間 80%

---

## 業界對標

→ 詳見 [05 痛點地圖 - 情境 7](../05-pain-points-industry-map.md#情境-7媒體業新聞輿情即時監測)

**過往學長姐 demo（最多參考的情境）**：
- [05 社群輿情分析（TIR103）](https://youtu.be/wECp8ge09YU)
- [10 誰是夜市水軍王（TJR101）](https://youtu.be/svH--o8U47I)
- [19 遊戲營運輿情智能資料管線系統（TJR104）](https://youtu.be/4oHXznCr6ls)
- [22 巴哈姆特輿情分析室（TJR104）](https://youtu.be/Bqvl2Nhgs3w)
- [02 NASA 精選天文圖之 LineBot（TIR102）](https://youtu.be/kg5TbuHKov0)

---

## 6 階段藍圖具體化

```
Source              Ingest             Storage         Transform         Serve              Observe
─────               ──────             ───────         ─────────         ─────              ───────
RSS feeds          requests +         MongoDB         LLM 分類+情緒      Streamlit          Sentry
NewsAPI            Airflow            (articles /     + 主題 cluster    + LINE Bot         + LLM cost
PTT / Threads      每 30 分           classified /    + 趨勢偵測         即時警示           + scrape
Google News API                       topics)                            主管推播           success rate
```

---

## 資料源細節

| 資料源 | 取得方式 | 規模 | 用來做 |
|---|---|---|---|
| [NewsAPI](https://newsapi.org/) | API（免費 100 req/day） | 各國新聞 | 主資料 |
| [Google News RSS](https://news.google.com/) | RSS | 中文新聞 | 在地化 |
| PTT 八卦 / Gossiping | 爬蟲 | 5000+/日 | 鄉民輿情 |
| Threads（透過第三方 API） | API | 限定品牌 mention | 社群即時 |

---

## 10 階段執行重點

### ① 啟動
- 選題理由：LLM 應用最直接、業界需求最大、demo 視覺效果好
- 適合選一個你有興趣的「品牌 / 議題」當主角

### ② Discovery
- Persona 範例：3C 品牌行銷經理小芳、每天上午掃 5 個媒體找品牌提及
- 痛點：(1) 跨平台分散 (2) 假日沒人盯 (3) 不知道議題在發酵

### ③ 設計
- 監控目標：品牌名 + 競品名 + 議題 keyword
- 分類：正面 / 負面 / 中性、議題類型（產品 / 服務 / 高層）
- 警示閾值：30 分鐘內負面提及 > X 觸發

### ④ 分工
| 角色 | 任務 |
|---|---|
| Ingest | NewsAPI + RSS + PTT 爬蟲 |
| Pipeline | Airflow 30 分 + LLM batch + cost |
| Analytics | 分類 prompt + 主題 cluster + 趨勢偵測 |
| Product | Streamlit + LINE Bot 警示 |

### ⑤ 環境
- LLM cost 控制最重要 — Sprint 1 就要建 budget

### ⑥ 衝刺

**Sprint 1（W10-W12）**：
- NewsAPI 抓 100 篇 → LLM 分類 → MongoDB
- 簡單 list 顯示

**Sprint 2（W13-W15）**：
- 加 PTT 爬蟲 + RSS
- 30 分鐘 Airflow
- 主題 clustering（每天自動分主題）
- Dashboard 雛形

**Sprint 3（W16-W18）**：
- 警示邏輯 + LINE Bot
- 趨勢圖（過去 30 天）
- Cost monitoring

### ⑦ 整合
- 端到端：新文章 30 分內進來 → 分類 → 趨勢分析 → 警示推播
- 整合測試：模擬「品牌爆雷」場景，看多久收到通知

### ⑧ 上線
- LINE Bot webhook 在 Cloud Run
- Streamlit + Airflow + MongoDB 在 GCP

### ⑨ Demo
最有殺傷力的 demo：
1. 開 dashboard 給 1 個月品牌輿情圖
2. 點某天高峰 → 看那天熱文 + 自動分類
3. **Live**：模擬一篇負面爆文進來 → LINE 立刻響
4. 講商業價值：「公關公司接 1 個客戶月費 5 萬，我這套替代 1 個分析師」

### ⑩ 復盤

---

## 範例：LLM 輿情分類 prompt

```python
SYSTEM = """你是品牌輿情分析師。針對給定文章，分析：
1. 情緒：positive / negative / neutral
2. 強度：1-5
3. 議題分類：product / service / management / pricing / other
4. 關鍵詞：3-5 個

如果文章未提及給定品牌則回傳 null。"""

USER = """品牌：{brand_name}
文章標題：{title}
文章內容：{content[:500]}"""

# Cost control：先用 gpt-4o-mini 篩，疑似負面才用 gpt-4o 細看
```

---

## 範例 commit log

```
* feat: NewsAPI ingest with keyword filter (#3)
* feat: PTT crawler for 八卦版 + Gossiping (#5)
* feat: MongoDB schema with text search (#7)
* feat: LLM sentiment + topic classifier (gpt-4o-mini) (#10)
* feat: 2-stage classifier - mini for filter, 4o for negative (#13)
* feat: topic clustering with sentence-transformers (#16)
* feat: LINE Bot push for critical alerts (#19)
* feat: streamlit dashboard with daily/weekly view (#22)
* perf: batch API saves 50% LLM cost (#25)
```

---

## 進階挑戰

- [ ] **Kafka streaming**：真正即時（30 秒延遲）
- [ ] **Vector DB**：主題追蹤跨日（看議題演化）
- [ ] **LLM 回應稿**：偵測到負面後自動 draft 回應
- [ ] **跨語言**：中英雙語監控 + 翻譯
- [ ] **多模態**：監測圖片 / 影片內容

---

## 雷區

| 雷 | 為什麼 |
|---|---|
| 每篇都 GPT-4 | 1 萬篇破萬元 |
| 警示閾值固定 | 假日 vs 平日不同 baseline |
| 沒去重 | 同則新聞被多個媒體轉，算多次 |
| RSS 部分 source 不更新 | 要監控 source health |

---

## 範例：cost control 策略

```
Tier 1 篩選（便宜）：
  - keyword matching（free）
  - gpt-4o-mini 分類（$0.15 / 1M tokens）
  ↓ 篩出疑似負面 5%

Tier 2 精細（貴）：
  - gpt-4o 深度分析（$2.5 / 1M tokens）

每天 10000 篇 × 95% × 0.15 + 10000 × 5% × 2.5
= $14.25 + $12.5 = ~$27 / 天

對比業界 SaaS 報價（千萬等級）：性價比 200x
```

---

## 完整時程（總 20 週）

| 週 | 階段 | 重點產出 |
|---|---|---|
| W1-W3 | 啟動 | 監控目標品牌選定 + LLM budget |
| W2-W4 | Discovery | 警示策略 + 分類體系 |
| W4-W7 | 設計 + 分工 | 2-stage classifier 設計 |
| W10-W12 | Sprint 1 | 100 篇通 + 分類 + 入庫 |
| W13-W15 | Sprint 2 | 多 source + 自動化 + cluster |
| W16-W18 | Sprint 3 | LINE 推播 + 趨勢 + cost monitor |
| W19 | 整合 + 上線 | end-to-end |
| W20 | Demo + 復盤 | live demo + 商業價值 |

---

← [上個情境：6 求職媒合](scenario-6-recruit.md) | 下個情境：[8 房地產 →](scenario-8-realestate.md)
