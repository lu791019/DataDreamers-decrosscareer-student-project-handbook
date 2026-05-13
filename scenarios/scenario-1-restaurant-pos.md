# 情境 1：餐飲連鎖 POS 庫存優化 + 熱銷分析

> **一句話**：給多門市餐廳老闆一個「今天該叫多少貨、哪個品項要退」的儀表板。

---

## 為誰解什麼

- **目標用戶**：3 家門市以上的餐飲連鎖店長 / 區域督導
- **痛點**：人腦記不住所有品項；憑感覺叫貨常常缺貨或過期
- **量化目標**：減少 X% 過期損耗、減少 Y% 缺貨次數、決策時間從 30 分鐘 → 3 分鐘

---

## 業界對標

→ 詳見 [04 痛點地圖 - 情境 1](../04-pain-points-industry-map.md#情境-1餐飲連鎖-pos)

**過往學長姐 demo**：
- [08 美味餐廳隨拾取（TIR104）](https://youtu.be/s2kePv2_A5I)
- [16 水果價格預測系統（TJR103）](https://youtu.be/nIjxkWHxT5k)
- [18 食喪地圖（TJR104）](https://youtu.be/FF9iNqWO9xw)
- [20 找咖小幫手（TJR104）](https://youtu.be/Oehs7Joi1cc)

---

## 6 階段藍圖具體化

```
Source                 Ingest              Storage         Transform          Serve           Observe
─────                  ──────              ───────         ─────────          ─────           ───────
Kaggle Restaurant     pandas              MySQL           pandas             Streamlit       Airflow UI
Order Details         + Airflow           (orders /       (groupby /         (店長/區督       + LINE notify
UCI Online Retail     每日 6am            inventory)      rolling avg)       /總部三視圖)     失敗推播
門市 POS export
```

---

## 資料源細節

| 資料源 | 取得方式 | 規模 | 用來做 |
|---|---|---|---|
| [Kaggle Restaurant Order Details](https://www.kaggle.com/datasets) | 下載 CSV | ~50 萬筆 | 訓練庫存模型 |
| [UCI Online Retail](https://archive.ics.uci.edu/dataset/352/online+retail) | 下載 CSV | ~50 萬筆 | 補充零售 pattern |
| 模擬門市 POS 資料 | 用 Faker 生 | 每門市每日 200-500 筆 | demo 用即時資料 |

---

## 10 階段執行重點

### ① 啟動
- 4 人組：1 ingest / 1 pipeline / 1 analytics / 1 product
- 選題理由：餐飲門檻低、資料公開、面試容易講故事

### ② Discovery
- Persona 範例：店長阿勇（45 歲、3 家分店、每天花 1 小時叫貨）
- 痛點：(1) 過期損耗 8%（業界平均 3%）(2) 缺貨頻率高 (3) 沒看每家門市差異

### ③ 設計
- 三層 schema：原始訂單 / 商品主檔 / 庫存狀態
- 三視圖 dashboard：店長日報 / 區督週報 / 總部品項熱度

### ④ 分工（範例）
| 角色 | 任務 |
|---|---|
| Ingest | Kaggle 載入 + 模擬即時資料 + 資料品質 |
| Pipeline | Airflow 排程 + MySQL schema + 升級 dbt |
| Analytics | 滑動平均 / 預測模型 / 補貨建議演算法 |
| Product | Streamlit 三視圖 + 部署 + demo |

### ⑤ 環境
fork [template-repo/](../template-repo/) → 改 README → 設定 GitHub Actions

### ⑥ 衝刺

**Sprint 1（W3）跑通**：
- ingest Kaggle CSV → MySQL → 跑一個 SQL 算出昨日 top 10
- Streamlit 顯示這個 top 10
- ✅ 端到端 1 條線

**Sprint 2（W4-5）擴充**：
- 加 Airflow 排程
- 加補貨建議演算法（7 日 SMA + 安全庫存）
- 三視圖切換

**Sprint 3（W6）打磨**：
- 加 dbt tests
- 加 LINE 失敗通知
- UI 優化

### ⑦ 整合
- 整合測試：模擬 3 天份資料跑完，dashboard 數字對得起來
- API 契約：ingest → MySQL 的 schema 凍結

### ⑧ 上線
- Streamlit Cloud 部署 dashboard
- Airflow 跑在 GCP Compute Engine（用學員額度）
- LINE Notify 監控

### ⑨ Demo
業務版 5 分鐘：
```
30 秒 - 「3 家店長每天花 1 小時叫貨，過期 8% 缺貨頻繁」
60 秒 - 「我們做了一個儀表板，3 分鐘給答案」
2 分鐘 - live demo（切換三視圖、模擬叫貨流程）
60 秒 - 「測試 1 個月後過期降到 3%、缺貨降 50%」
30 秒 - CTA
```

### ⑩ 復盤
詳見 [05](../05-retro-and-after.md)

---

## 範例 commit log（業界等級）

```
* feat: add daily order ingest from Kaggle CSV (#3)
* feat: design MySQL schema for orders/inventory/products (#5)
* test: add unit tests for inventory_calc module (#7)
* feat: implement 7-day SMA replenishment algorithm (#9)
* fix: handle empty order date in raw CSV (#11)
* docs: add architecture diagram and ER diagram (#12)
* feat: add Airflow DAG for daily 6am refresh (#14)
* refactor: split analytics module into staging/intermediate/mart (#17)
* feat: integrate LINE Notify for pipeline failures (#19)
* feat: 3-view dashboard - store/regional/HQ (#21)
* ci: add docker-compose health check in CI (#23)
* docs: update README with deployment guide (#25)
```

---

## 範例 PR description

```markdown
## 這個 PR 做什麼
實作 7 日滑動平均補貨建議演算法 + 整合進 daily DAG

## 為什麼
Sprint 2 目標的核心功能。原本只有「昨日熱銷」，現在能給出「明天該叫多少」。

## 怎麼測試
- pytest tests/analytics/test_replenishment.py — 8 cases all pass
- 手動跑 Airflow DAG，inventory_view 表正確產出
- 比對 store_1 三天份模擬資料，建議結果合理

## 截圖
[補貨建議表格截圖]

## 影響範圍
- 新增 src/analytics/replenishment.py
- 新增 tests/analytics/test_replenishment.py
- 修改 dags/daily_pipeline.py 加 task
- 沒改 schema

Closes #9
```

---

## 進階挑戰（想拉滿分加這些）

- [ ] 加 **LLM 評論分析**：抓 Google Maps 評論做情緒分類 → 結合銷售看「品項 vs 評論」
- [ ] 加 **天氣 API**：天氣冷 → 火鍋類自動加成補貨建議
- [ ] 加 **dbt + BigQuery**：把 Transform 層重寫成 dbt models
- [ ] 加 **異常偵測**：銷量突然掉 50% 自動 alert

---

## 雷區（千萬別這樣）

| 雷 | 為什麼 |
|---|---|
| 只做「昨日熱銷報表」 | 太薄，業界要的是「決策建議」 |
| schema 設計不分層 | 改個欄位就全炸 |
| 沒考慮多門市差異 | 一家店模型，所有店都用＝結論很爛 |
| 用 Kaggle 資料就直接 demo | 要混入「模擬即時」資料才看得出 pipeline 價值 |

---

## 範例 retro 紀錄

```markdown
# Sprint 2 Retro - 2026-04-12

## Keep
- 大家用 PR 不直接 push main 後，少很多衝突
- 阿凱的 Airflow 排程一次寫好沒重做

## Problem
- Schema 改動沒先講，小美整天 work 卡掉
- Demo 用的模擬資料生得太少（一天 50 筆）看不出趨勢

## Try
- Schema 改動先開 issue 標 [schema-change]
- 寫一個 fake data 生成器一次生 30 天份
```

---

## 完整時程（總 8 週）

| 週 | 階段 | 重點產出 |
|---|---|---|
| W0 | 啟動 | team charter / 選定本情境 |
| W1 | Discovery | persona / data inventory |
| W2 | 設計 + 分工 | 4 張圖 / RACI |
| W3 | Sprint 1 | 跑通 ingest → MySQL → Streamlit |
| W4-5 | Sprint 2 | 排程 + 補貨演算法 + 三視圖 |
| W6 | Sprint 3 | 監控 + 文件 + LINE notify |
| W7 | 整合 + 上線 | docker compose / 雲端部署 |
| W7-8 | Demo + 復盤 | dry run × 3 / 個人 retro |

---

← [回到 README](../README.md) | 下一個情境：[2 電商比價 →](scenario-2-ecommerce.md)
