# 情境 5：叫車服務交通熱點 + 車輛調度

> **一句話**：給叫車平台調度組「未來 30 分鐘哪個區會缺車、要不要加價」的預測系統。

---

## 為誰解什麼

- **目標用戶**：叫車 / 外送平台調度部門 / 物流公司運能規劃
- **痛點**：尖峰時段叫不到車、司機跑空車、加價策略憑感覺
- **量化目標**：缺車預測準確度 ≥ 80%；司機空車率降 15%

---

## 業界對標

→ 詳見 [05 痛點地圖 - 情境 5](../05-pain-points-industry-map.md#情境-5叫車服務交通熱點--車輛調度)

**過往學長姐 demo**：
- [13 國道車流 LSTM（TJR102）](https://youtu.be/uZMLE1ebBI0)
- [11 國旅推薦（TJR101）](https://youtu.be/C7HAXjmqFIY)

---

## 6 階段藍圖具體化

```
Source                  Ingest             Storage         Process        Serve            Observe
─────                   ──────             ───────         ─────────        ─────            ───────
NYC TLC Trip Records   下載 + Airflow     BigQuery        BigQuery GIS     FastAPI          Airflow UI
Uber Movement          每 15 分鐘         (raw_trips /     + Python LSTM    + Streamlit       + BigQuery
台北 ETC 公開資料                          aggregated /                      地圖儀表板       cost monitor
                                          predictions)
```

---

## 資料源細節

| 資料源 | 取得方式 | 規模 | 用來做 |
|---|---|---|---|
| [NYC TLC Yellow/Green Taxi](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page) | 下載 parquet | 月 ~1 GB / 數百萬筆 | 主要資料 |
| [Uber Movement](https://movement.uber.com/) | API / 開放下載 | 城市行程時間 | 補充交通 |
| [台北 ETC 公開資料](https://data.gov.tw/dataset/93358) | 政府開放資料 API | 即時車流 | 在地化 demo |

---

## 10 階段執行重點

### ① 啟動
- 選題理由：時序預測 + 地理空間 = DE 進階技術全包
- 注意：地理計算很吃資源，預算 BigQuery cost

### ② Discovery
- Persona 範例：Uber 台北調度組長（4 人團隊、200 司機）
- 痛點：(1) 尖峰被罵叫不到 (2) 司機跑空車離峰 (3) 加價策略缺數據支撐

### ③ 設計
- 地理切分：H3 hexagon（Uber 內部就在用）
- 時間切分：每 15 分鐘 bucket
- 預測模型：LSTM / Prophet / XGBoost 三選一

### ④ 分工
| 角色 | 任務 |
|---|---|
| Ingest | TLC 資料下載 + ETC API + BigQuery loader |
| Pipeline | Airflow 15min 更新 + dbt models |
| Analytics | LSTM 預測 + 評估 + 熱點演算法 |
| Product | Streamlit 互動地圖 + FastAPI |

### ⑤ 環境
- BigQuery 用學員 GCP 額度（注意 cost）
- 地圖：用 pydeck / folium 不要從零做

### ⑥ 衝刺

**Sprint 1（W10-W12）**：
- 1 個月 TLC 資料載進 BigQuery
- 跑出「過去 30 天每小時 H3 hex 行程數」
- 簡單地圖顯示

**Sprint 2（W13-W15）**：
- Airflow 每 15 分鐘 incremental update
- LSTM 訓練 + 預測未來 30 分鐘
- 預測 vs 實際對照

**Sprint 3（W16-W18）**：
- FastAPI `/predict?lat=&lng=&minutes=` endpoint
- Streamlit 熱點地圖 + 預測切換
- 加 BigQuery cost monitoring

### ⑦ 整合
- 端到端：新時段資料進來 → LSTM 跑 → API 給最新預測
- 整合測試：模擬「司機 app 來呼叫 API」

### ⑧ 上線
- BigQuery 在 GCP
- FastAPI 在 Cloud Run
- Streamlit 在 Streamlit Cloud

### ⑨ Demo
強調「**真實業界規模感**」：
1. 講資料量：「我們處理 1 億筆行程」（demo 印象深）
2. 對比預測 vs 實際：「準確度 82%」
3. Live demo：模擬 demo day 時段 → 預測

### ⑩ 復盤

---

## 範例：H3 hexagon 切分

```python
import h3

def trip_to_hex(lat, lng, resolution=9):
    """resolution 9 約 = 0.1 km^2 一格，適合都會區"""
    return h3.geo_to_h3(lat, lng, resolution)

# BigQuery 上的 SQL
"""
SELECT
  h3_hex_from_geog(pickup_geog, 9) AS hex,
  TIMESTAMP_TRUNC(pickup_datetime, MINUTE, "UTC") - INTERVAL MOD(EXTRACT(MINUTE FROM pickup_datetime), 15) MINUTE AS time_bucket,
  COUNT(*) AS trip_count,
  AVG(fare_amount) AS avg_fare
FROM `nyc-tlc.trips`
WHERE pickup_datetime >= TIMESTAMP_SUB(CURRENT_TIMESTAMP(), INTERVAL 30 DAY)
GROUP BY 1, 2
"""
```

---

## 範例 commit log

```
* feat: ingest NYC TLC parquet to BigQuery (#3)
* feat: H3 hex aggregation with 15min time buckets (#7)
* feat: LSTM model with 24h lookback (#11)
* test: model evaluation MAE/RMSE on holdout (#13)
* feat: FastAPI /predict endpoint (#16)
* feat: Streamlit interactive hex map with pydeck (#19)
* perf: incremental BigQuery refresh saves 70% cost (#22)
* docs: ADR-004 - why LSTM over Prophet (#24)
```

---

## 進階挑戰

- [ ] **Kafka + Spark Streaming**：真即時（每秒 update）
- [ ] **多模態預測**：加天氣 / 活動 / 事件
- [ ] **動態加價演算法**：給司機 app 即時建議
- [ ] **司機路線優化**：給定當前位置，10 分鐘後該往哪移

---

## 雷區

| 雷 | 為什麼 |
|---|---|
| BigQuery 沒分區 | scan 全表 cost 爆炸 |
| 用 lat/lng 直接 group by | 太細沒意義 |
| LSTM 訓練資料 < 1 個月 | 學不到 weekly pattern |
| 地圖太多點 | 瀏覽器卡死 |

---

## 完整時程（總 20 週）

| 週 | 階段 | 重點產出 |
|---|---|---|
| W1-W3 | 啟動 | GCP 額度 + BigQuery setup |
| W2-W4 | Discovery | H3 切分策略 |
| W4-W7 | 設計 + 分工 | schema + 模型選型 |
| W10-W12 | Sprint 1 | 1 月資料 + 地圖 |
| W13-W15 | Sprint 2 | 自動化 + LSTM + 評估 |
| W16-W18 | Sprint 3 | API + 互動地圖 + cost monitor |
| W19 | 整合 + 上線 | end-to-end |
| W20 | Demo + 復盤 | 強調規模 + 預測準確度 |

---

← [上個情境：4 音樂串流](scenario-4-music.md) | 下個情境：[6 求職媒合 →](scenario-6-recruit.md)
