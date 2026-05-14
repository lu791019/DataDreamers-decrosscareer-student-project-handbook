# 情境 2：B2C 電商競品比價 + 動態定價

> **一句話**：給電商運營一個「我家商品在市場排第幾、要不要調價」的決策工具。

---

## 為誰解什麼

- **目標用戶**：電商品牌商運營經理 / 通路品牌經理
- **痛點**：手動查競品價格費時、價格戰反應慢、不知道什麼時機降價
- **量化目標**：監控時間從每週 4 小時 → 0；自動建議定價的精準度 ≥ 70%

---

## 業界對標

→ 詳見 [05 痛點地圖 - 情境 2](../05-pain-points-industry-map.md#情境-2b2c-電商競品比價--動態定價)

**過往學長姐 demo**：
- [16 水果價格預測系統（TJR103）](https://youtu.be/nIjxkWHxT5k)

---

## 6 階段藍圖具體化

```
Source              Ingest              Storage          Process          Serve            Observe
─────               ──────              ───────          ─────────          ─────            ───────
momo / PChome      Scrapy/             MySQL            pandas + SQL       FastAPI           Sentry
蝦皮 / Yahoo       Playwright          (prices/         (時序處理 /         + Streamlit       + 排程監控
品牌商商品 list    Airflow 每小時      products/        定價建議模型）       (兩端：API        + 反爬蟲 alert
                                       brand_skus)                          給品牌系統用)
```

---

## 資料源細節

| 資料源 | 取得方式 | 規模 | 用來做 |
|---|---|---|---|
| momo 商品頁 | Scrapy + rotating user-agent | 1000 SKU × 4 平台 | 競品價格 |
| PChome 24h | Playwright（動態 JS） | 同上 | 競品價格 |
| 蝦皮 | API（公開的 search endpoint） | 同上 | 競品價格 |
| 自家品牌 SKU 對照表 | 手動建（學員用模擬資料） | 50-100 SKU | SKU 對齊 |

---

## 10 階段執行重點

### ① 啟動
- 選題理由：爬蟲是 DE 必修；競品比價是品牌商最痛的需求
- 強烈建議：選一個你「真的會買」的品類（保健食品 / 3C / 化妝品）

### ② Discovery
- Persona 範例：品牌經理小芸（保健食品品牌、月做 ¥500 萬）
- 痛點：(1) 競品降價她兩天後才知道 (2) 老闆每週要 5 個競品的價格 Excel (3) 不知道調價對銷量的影響

### ③ 設計
- 關鍵：**SKU 對齊問題**（「魚油 60 粒」vs「魚油深海 60 顆」是同一商品嗎？）
- 三層：raw scrape → product_match → price_intelligence

### ④ 分工
| 角色 | 任務 |
|---|---|
| Ingest | 4 平台爬蟲 + 反爬蟲處理 |
| Pipeline | Airflow 每小時 + retry 邏輯 |
| Analytics | SKU 對齊（embedding match）+ 定價建議 |
| Product | API + Streamlit + 警示推播 |

### ⑤ 環境
注意：`.gitignore` 要加 `data/raw/` — 不要 commit 爬到的內容！

### ⑥ 衝刺

**Sprint 1（W10-W12）跑通**：
- 1 個平台 + 10 個 SKU 爬通
- MySQL 存
- 一個簡單 line chart

**Sprint 2（W13-W15）擴充**：
- 4 個平台
- SKU 對齊（用 sentence-transformers embedding）
- Airflow 每小時

**Sprint 3（W16-W18）打磨**：
- 加定價建議邏輯
- 加 Sentry 監控爬蟲失敗
- FastAPI 暴露給「品牌的內部系統」用

### ⑦ 整合
- 重點：模擬「品牌內部系統來呼叫 API 取得建議價」的場景
- 整合測試：給定 SKU，能拿到 4 個平台價格 + 建議價

### ⑧ 上線
- API 部署 GCP Cloud Run
- Dashboard 部署 Streamlit Cloud
- Sentry 接 Slack alert

### ⑨ Demo
強調「**從手動 → 自動 → 智能**」三段：
1. 業界現況：人工 Excel
2. 我們的解：自動化爬蟲
3. 進階：embedding 對齊 + 建議

### ⑩ 復盤

---

## 範例 commit log

```
* feat: scrapy spider for momo search results (#3)
* feat: handle PChome dynamic JS with playwright (#5)
* fix: respect robots.txt and add 2s sleep between requests (#7)
* feat: MySQL schema for prices/products with daily snapshot (#9)
* feat: SKU matching using sentence-transformers embeddings (#12)
* feat: dynamic pricing recommendation v1 (cost+margin) (#15)
* feat: Airflow hourly DAG with retry + sentry integration (#18)
* feat: FastAPI endpoint /price-suggestion/{sku_id} (#21)
* docs: anti-scraping playbook (cookies/UA/rate limit) (#23)
```

---

## 範例 issue

```markdown
title: [bug] momo 商品下架時爬蟲被 ban

## 重現步驟
1. SKU id 12345 已下架
2. spider 抓到 404
3. 連續 5 個 404 後整個 spider 被 momo CDN 擋了

## 預期
404 應該 skip + log，不該觸發 ban

## 實際
被擋 1 小時

## 建議
- 404 直接 skip
- 5xx 才 retry
- 加 random sleep 2-5 秒
- 用 rotating proxy

labels: bug, sprint-2, ingest
assignee: @dex
```

---

## 進階挑戰

- [ ] **CDC（Debezium）即時**：競品降價 5 分鐘內知道
- [ ] **ML 預測競品下次降價**：時序分析
- [ ] **A/B test 定價建議**：模擬不同策略的銷量
- [ ] **多模態 SKU match**：用商品圖加上文字 embedding

---

## 雷區

| 雷 | 為什麼 |
|---|---|
| 爬太狠把對方擋掉 | 法律問題 + 你資料中斷 |
| SKU 對齊用「商品名稱完全相等」 | 對不到 95% |
| 沒紀錄歷史價格 | 沒辦法分析趨勢 |
| 只給「現在最便宜」 | 那 PC 比價網就好了，沒競爭力 |

---

## 重要：合規 disclaimer

爬蟲務必：
- 遵守 `robots.txt`
- 加 `User-Agent` 表明身份（甚至附 email）
- 速率限制（每秒 < 1 request）
- 不要 commercial use 沒授權的資料

---

## 完整時程（總 20 週）

| 週 | 階段 | 重點產出 |
|---|---|---|
| W1-W3 | 啟動 | 選定品類 |
| W2-W4 | Discovery | persona + 4 個平台站圖 |
| W4-W7 | 設計 + 分工 | scrapy 架構 + SKU 對齊方案 |
| W10-W12 | Sprint 1 | 1 平台 10 SKU 通 |
| W13-W15 | Sprint 2 | 4 平台 + SKU match + Airflow |
| W16-W18 | Sprint 3 | 定價建議 + FastAPI + 監控 |
| W19 | 整合 + 上線 | Cloud Run + Streamlit Cloud |
| W20 | Demo + 復盤 | 強調自動化價值 |

---

← [上個情境：1 餐飲 POS](scenario-1-restaurant-pos.md) | 下個情境：[3 數位金融 →](scenario-3-fintech.md)
