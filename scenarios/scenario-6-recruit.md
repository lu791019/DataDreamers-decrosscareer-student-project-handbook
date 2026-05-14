# 情境 6：求職媒合職缺趨勢 + 薪資洞察

> **一句話**：給求職者一個「我學這個技能薪水多少、市場缺多少人、未來趨勢」的決策儀表板。

---

## 為誰解什麼

- **目標用戶**：轉職者 / 應屆畢業 / 求職者 / HR
- **痛點**：選技能憑感覺、不知道市場熱度、薪資談判沒參考
- **量化目標**：覆蓋 80% 主流職位、薪資中位數誤差 < 15%

---

## 業界對標

→ 詳見 [04 痛點地圖 - 情境 6](../04-pain-points-industry-map.md#情境-6求職媒合職缺趨勢--薪資洞察)

**過往學長姐 demo**：
- [04 求職 360°（TIR103）](https://youtu.be/fCuxt4RLiiM)
- [21 求職求值（TJR104）](https://youtu.be/E3ZEGIouwv4)

---

## 6 階段藍圖具體化

```
Source                  Ingest             Storage         Transform         Serve            Observe
─────                   ──────             ───────         ─────────         ─────            ───────
104 / CakeResume       Playwright         MongoDB          pandas + LLM       Streamlit        Sentry
LinkedIn (lite)        + Scrapy           (raw_jobs /      (技能抽取 /        + Tableau /       + scrape
勞動部統計              Airflow daily      jobs_clean /     薪資 parse /       Looker Studio    success rate
GitHub Jobs API                            skills_index)    embedding match）  互動式           monitor
```

---

## 資料源細節

| 資料源 | 取得方式 | 規模 | 用來做 |
|---|---|---|---|
| 104 人力銀行 | Playwright（反爬蟲硬）| 每天 2-5 萬職缺 | 主資料 |
| [CakeResume](https://www.cakeresume.com/) | Scrapy | 每天 5000 職缺 | 補充科技業 |
| [勞動部薪資統計](https://www.mol.gov.tw/) | API / Excel | 各行業中位數 | 校準 |

---

## 10 階段執行重點

### ① 啟動
- 選題理由：HR Tech 熱門、轉職者自己用得到、爬蟲 + NLP 全棧
- 注意：104 反爬蟲很硬，要做好心理建設

### ② Discovery
- Persona 範例：轉職者阿宏 30 歲、傳產 → DE、不知道學什麼能加薪
- 痛點：(1) 線上課程太多選不出 (2) 不知道現在學的技能 3 年後還熱不熱 (3) 不知該開多少薪水

### ③ 設計
- 技能 taxonomy：分 hard skills / soft skills / tools / domains
- 薪資 parsing：「面議」「30K-50K」「年薪」要分類處理
- 三層：raw → cleaned → indexed (skills, salary, location)

### ④ 分工
| 角色 | 任務 |
|---|---|
| Ingest | 104 / CakeResume 爬蟲 + 反制 |
| Pipeline | Airflow daily + retry + 去重 |
| Analytics | LLM 技能抽取 + 薪資 parsing + 趨勢分析 |
| Product | Streamlit 多視圖 + 個人化推薦 |

### ⑤ 環境
- 104 要 cookie / session 處理
- 用 `playwright-stealth` 降低被檢測機率

### ⑥ 衝刺

**Sprint 1（W10-W12）**：
- 1000 個 DE 職缺爬通 → MongoDB
- 簡單 dashboard 顯示薪資分佈

**Sprint 2（W13-W15）**：
- LLM 抽技能（從職缺描述）
- 多職缺類型（DE / SWE / DA / DS）
- Airflow 自動化

**Sprint 3（W16-W18）**：
- 技能熱度排行（時序）
- 個人化推薦（給定技能組合，看哪個職缺 match）
- 對比勞動部數據校準

### ⑦ 整合
- 端到端：新職缺 → 抽技能 → 入庫 → dashboard 更新
- 整合測試：用 100 個已標註職缺，看 LLM 抽技能準確度

### ⑧ 上線
- Streamlit Cloud
- Airflow / MongoDB 在 GCP

### ⑨ Demo
強調「**轉職者真的用得到**」：
1. 開 dashboard，輸入「我會 Python + SQL」
2. 顯示：(a) 對應職缺 X 個 (b) 薪資中位數 Y (c) 補學 Z 技能薪水可以 +30%
3. 講你自己（demoer）就是用戶

### ⑩ 復盤

---

## 範例：LLM 技能抽取

```python
SYSTEM = """從職缺描述中抽取「技能」並分類為：
- language: 程式語言
- framework: 框架 / library
- tool: 工具 / 平台
- domain: 領域知識
- soft: 軟技能

回傳 JSON。如果無法判斷，標記為 unknown。"""

EXAMPLE = """
輸入：「熟悉 Python、Pandas、Airflow，了解資料倉儲概念，有 GCP 經驗者優先」
輸出：[
  {"skill": "Python", "type": "language", "required": true},
  {"skill": "Pandas", "type": "framework", "required": true},
  {"skill": "Airflow", "type": "tool", "required": true},
  {"skill": "資料倉儲", "type": "domain", "required": true},
  {"skill": "GCP", "type": "tool", "required": false}
]
"""
```

---

## 範例 commit log

```
* feat: 104 playwright scraper with session handling (#3)
* fix: handle "面議" salary parsing edge case (#6)
* feat: MongoDB schema with full-text search index (#9)
* feat: LLM skill extraction with 5 categories (#12)
* test: extraction accuracy eval - 89% on 200 jobs (#14)
* feat: skill trend analysis with 30-day rolling (#17)
* feat: streamlit personalized recommendation (#20)
* feat: tableau dashboard for HR-facing view (#23)
* docs: anti-scraping decisions ADR-005 (#25)
```

---

## 進階挑戰

- [ ] **Embedding + Vector DB**：履歷 vs 職缺 semantic match
- [ ] **知識圖譜**：技能之間的依賴關係（Pandas → NumPy → Python）
- [ ] **LLM 自動寫履歷**：給定職缺 + 你的背景，自動生 cover letter
- [ ] **薪資談判建議**：基於數據給談判話術

---

## 雷區

| 雷 | 為什麼 |
|---|---|
| 104 爬太快被擋 | sleep + random + rotating UA |
| 技能 taxonomy 太細 | 「Python 3.9」vs「Python 3.10」算同一個 |
| 沒做去重 | 同職缺重複上架算多次 |
| 薪資全部當數字 | 「面議」「年薪」要 normalize |

---

## 重要：法律風險

爬蟲 104 屬於「灰色地帶」：
- 不做 commercial use 一般沒事
- 不要 publish 個人資料
- 學習目的、demo 用 OK
- 履歷上寫專案 OK
- 但**不要做成 SaaS 開賣**

---

## 完整時程（總 20 週）

| 週 | 階段 | 重點產出 |
|---|---|---|
| W1-W3 | 啟動 | 法律 / 倫理討論 |
| W2-W4 | Discovery | persona + 技能 taxonomy |
| W4-W7 | 設計 + 分工 | 爬蟲架構 + 反制策略 |
| W10-W12 | Sprint 1 | 1000 職缺爬通 |
| W13-W15 | Sprint 2 | LLM 技能抽取 + 自動化 |
| W16-W18 | Sprint 3 | 趨勢 + 推薦 |
| W19 | 整合 + 上線 | dashboard 部署 |
| W20 | Demo + 復盤 | 強調轉職者價值 |

---

← [上個情境：5 叫車交通](scenario-5-ride.md) | 下個情境：[7 新聞輿情 →](scenario-7-news.md)
