# 專案協作第 3 週 ｜ 03 小組專案 10 階段流程

> 這是把整個課程的小組專案做完的完整 SOP。每階段都有：**目標 / 產出物 / 時間預算 / 卡關處方 / 建議**。

> 📅 **TibaMe 20 週節奏**
> 前 8-9 週基礎技術課同時進行專題前置和確認（討論 / 規劃 /  工具配置 / 情境選定 / 角色分工確認）
> 後 11 週進階課程同時專題實作（衝刺 / 整合 / Demo）

---

## 全景圖

```
階段                              時間           重點
─────────────────────────────────────────────────────────────
前置期（基礎技術課 + 專題醞釀，每週 2-3 hr）
W1-W3   ① 啟動               組隊 / 選題 / 簽契約
W2-W4   ② Discovery          用戶 / 痛點 / 資料盤點
W4-W6   ③ 設計               架構圖 / ER 圖 / API 契約
W5-W7   ④ 分工               RACI / 模組 owner 認領
W7-W9   ⑤ 環境               GitHub repo + 溝通工具 + PM 工具

實作期（進階課程 + 專題開發，每週 8-12 hr）
W10-W12 ⑥-1 Sprint 1         端到端跑通最小可行 pipeline
W13-W15 ⑥-2 Sprint 2         擴充 + 自動化
W16-W18 ⑥-3 Sprint 3         打磨 + 監控
W19     ⑦ 整合 + ⑧ 上線      docker compose / 部署 / 文件
W20     ⑨ Demo + ⑩ 復盤      練稿 / dry run / retro / 履歷升級
```

> 階段時間略有重疊是刻意的：前置期 5 件事可以並行推進，不必嚴格線性。

---

## ① 啟動（Week 1 - Week 3）

### 目標
**確定組員、選定題目**。

### 產出物
- `team-charter.md`：組員名單 / 強項 / 弱項 / 時區 / 每週可投入時數
- `topic-decision.md`：選了哪個情境、為什麼選、目標用戶
- 一個共用通訊工具（Slack / Discord / LINE ）

### 時間預算
- 1.5 hr：互相認識 + 強項盤點
- 1.5 hr：8 情境選題

### 卡關處方

| 卡關 | 處方 |
|---|---|
| 都選最熱門題目 | 看 04 痛點地圖 — 哪題對「你過去職涯」最有故事 |
| 大家都想當 lead | 用 RACI 分工，沒有「lead」只有 4 種角色 |

### 建議
- **選題比技術重要**：選一個「面試時你能講 5 分鐘為什麼選」的題目，遠比「最潮的題目」有用
- **不要為了平均而平均**：組員都「平均做 25%」反而會讓專案缺乏深度，讓強項極大化、互補弱項

---

## ② Discovery（Week 2- Week 3，約 8 小時）

### 目標
**搞清楚：誰在用、為什麼用、痛在哪、資料怎麼來**。

### 產出物
- `docs/user-persona.md`：1-2 個具體 persona（不是「年輕人」這種太模糊的描述）
- `docs/pain-points.md`：3-5 個具體痛點（要可量化）
- `docs/data-inventory.md`：所有可能資料來源清單（含取得難度評估）

### 時間預算
- 3 hr：訪談 / 看現有報告 / 蒐集資料
- 2 hr：了解 persona (客戶畫像、TA樣貌)、痛點和市場描述)
- 3 hr：盤點資料來源 

### Persona 範例（具體 vs 模糊）

❌ **太模糊**：「年輕的音樂愛好者」
✅ **好**：
```
姓名：阿凱，26 歲，新北
工作：行銷 AE，月薪 4 萬
聽歌時段：通勤 7-8am、健身 7-9pm
痛點：每天 Spotify 推薦都同質化，新歌很少被推到；
       想找跟最近聽的歌「氛圍類似但沒聽過」的歌
願付：免費，但會看 2-3 個廣告換功能
```

### 卡關處方

| 卡關 | 處方 |
|---|---|
| 「我們又沒目標用戶」 | 你自己就是用戶 — 寫你自己的需求 |
| 找不到資料 | 看 01 藍圖 Source 段和 8 種情境  |
| 痛點寫得很抽象 | 加數字：「每天平均花 X 分鐘做 Y」 |

---

## ③ 設計 （Week 4 - Week 5）

### 目標
**畫出系統長什麼樣**。

### 產出物（4 張圖一份文件）
1. `docs/architecture.md` — 系統架構圖（6 階段藍圖具體化）
2. `docs/data-flow.md` — 資料流向圖（誰餵誰）
3. `docs/er-diagram.md` — ER 圖 / NoSQL schema
4. `docs/api-contract.md` — 模組間 API 契約

### 工具
- **draw.io**（推薦）：免費 + 跟 GitHub 整合
- **Excalidraw**：手繪風，討論用最舒服
- **Mermaid**：直接寫在 markdown，PR 看得到 diff
- **dbdiagram.io**：ER 圖專用

### 為什麼要先畫？
> 「在 whiteboard 上花 1 小時，省 10 小時打 code。」

設計階段發現的問題：免費。
寫到一半發現的問題：要重構。
demo 前發現的問題：要熬夜。

### 卡關處方

| 卡關 | 處方 |
|---|---|
| 不會畫架構圖 | 抄 01 藍圖那張圖，把工具名換成你的 |
| schema 設計卡住 | 先想 query：「我要回答什麼問題？」反推欄位 |

---

## ④ 分工（Week 6，約 2 小時）

### 目標
**讓每個人有清楚的 ownership，但沒人是孤島**。

### 4 種角色（不是 1 種）

| 角色 | 職責 | 適合的人 |
|---|---|---|
| **Data Ingest Owner** | 資料來源確認 / API / 資料品質 | 細心、抗錯耐性高 |
| **Pipeline Owner (ETL Engineer)** | Airflow / Docker / 排程 | 喜歡自動化 |
| **Analytics Owner** | SQL / pandas / 模型 | 數理直覺好 |
| **Product Owner** | Streamlit / API / UX | 會講故事、會 demo |

> **每人主擔 1 個 + 副擔 1 個**

### RACI 矩陣（範例 — 3 人組）

| 任務 | 組員 A | 組員 B | 組員 C |
|---|---|---|---|
| 爬蟲開發 | **R** | C | A |
| Airflow 排程 | C | **R** | A |
| 分析模型 | A | C | **R** |
| Streamlit | A | **R** | C |
| Code Review | C | C | C |

> 3 人組面對 4 個模組角色，每人會主擔 1 個 + 副擔 1 個（例如 A 主擔 Ingest 副擔 Product；B 主擔 Pipeline 副擔 Product；C 主擔 Analytics 副擔 Pipeline）。
> 角色不是「人」，是「職責」 — 一人可以兼。

> R = Responsible（動手）／ A = Accountable（負責）／ C = Consulted（要問）／ I = Informed（要告知）

### 卡關處方

| 卡關 | 處方 |
|---|---|
| 有人攬太多 | 約定每人最多 1 個 R（避免 burn out）|
| 沒人想做 Product Owner | 這個角色面試時往往最受訪，組內可以一起扛 |

---

## ⑤ 環境（W7-W9）

### 目標
**把基建一次架好 — 後面 11 週就不用回頭調**。

### 產出物
- GitHub repo 建好（看 [01 章 SOP](01-github-setup-sop.md) 一般版或專業版）
- 溝通工具（Discord / Slack / LINE）+ channels 建好（看 [00 章](00-agile-and-tools.md)）
- PM 工具（GitHub Projects / Trello / Linear）設好
- Branch 規範：`main` / `develop` / `feature/*` / `fix/*`
- 第一個 PR 跑通 CI
- README / PLAN / task.md 三件套

### 細節展開
- Git 與 PR 流程 → [05 業界協作 SOP](05-collaboration-sop.md)
- 工具選型 → [00 敏捷開發與工具選型](00-agile-and-tools.md)

> 前置期最後 2-3 週的事，慢慢架不要硬塞一天。

---

## ⑥ 衝刺（W10-W18 專案開發衝刺期）

> 這節是 [00 章敏捷方法論（Scrumban）](00-agile-and-tools.md) 的具體應用。
> 如果還不熟 Scrumban 三大支柱（看板 / Planning / Review），先回去翻 02 再回來。

### 節奏（雙週 sprint，3 個 sprint × 3 週 ≈ 9 週實作期）
```
Sprint 開始日   sprint planning (60 min)   決定本期要做什麼   ← 00 章 Sprint Planning
每天 09:30      異步 daily check（文字）    我做什麼 / 卡什麼  ← 00 章 Daily Check-in
Sprint 結束日   sprint review (60 min)     demo 給組內看      ← 00 章 Sprint Review
（不做 sprint retro，學期末一次 final retro 即可，看 06 章）
```

### Sprint 1（W10-W12，3 週）：跑通最小可行 pipeline
- 目標：**端到端跑得起一遍**，醜沒關係
- 完成度：Source → Storage → 一個結果（哪怕是 print）
- 提醒：花 3 週把爬蟲調到完美 → demo 沒得展。**先跑通整條再回頭優化**

### Sprint 2（W13-W15，3 週）：擴充 + 自動化
- 目標：加排程 + 加更多資料源 + 加分析
- 完成度：能每天自動跑、有 dashboard 雛形

### Sprint 3（W16-W18，3 週）：打磨 + 監控
- 目標：UI 順、有監控、文件齊
- 完成度：別人能自己跑起來

### 卡關處方

| 卡關 | 處方 |
|---|---|
| 進度落後 | **砍 scope** 不是熬夜 — 砍掉 next-to-have |
| 有人神隱 | 馬上 escalate 給教練，不要拖 |
| 一直 refactor | sprint 中禁 refactor，sprint review 才討論 |

---

## ⑦ 整合（W17-W18）

### 目標
**把組員各自寫的 code 串成一個 pipeline**。

### 整合 checklist
- [ ] 所有模組能用 `docker compose up` 一鍵起來
- [ ] 模組間 API 契約都符合（用 schema validation）
- [ ] 端到端跑一次：source → dashboard 看得到結果
- [ ] CI 跑得過

### 卡關處方

| 卡關 | 處方 |
|---|---|
| 模組對不上 | 回去看 `docs/api-contract.md` — 沒有就現在補 |
| Docker 起不來 | 用 docker compose 不要每人各自 docker run |
| 跑一次要 10 分鐘 | 先有再快 — 等 demo 前再優化 |

---

## ⑧ 上線（W17-W18）

### 目標
**讓別人在你的 demo 之外，能自己玩你的系統**。

### 部署選項

| 平台 | 費用 | 適合 |
|---|---|---|
| GCP Cloud Run | 免費額度夠 | API / Streamlit |
| Vercel | 免費 | 純前端 |
| Render | 免費 | 小型服務 |
| Streamlit Cloud | 免費 | dashboard |
| GCP Compose Engine | 學員額度 | Airflow / 整套 |

### 監控最低門檻
- [ ] Pipeline 跑失敗 → 至少 LINE / Email 通知一下
- [ ] Dashboard 上有「最後更新時間」
- [ ] 有 health check endpoint

---

## ⑨ Demo（W19）

### 兩種 demo

| 版本 | 對象 | 重點 | 時長 |
|---|---|---|---|
| **業務版** | 老闆 / 面試官 / 投資人 | 解了什麼問題、影響多大 | 5 min |
| **技術版** | 同行 / 教練 / 工程主管 | 怎麼解、架構選型、踩過什麼坑 | 10 min |

### Demo 結構（業務版 5 分鐘）
```
30 秒：痛點 — 「現在你做這件事要花 X 分鐘 / 元」
60 秒：方案 — 「我們做了 X，你只要 Y」
2 分鐘：live demo
60 秒：影響 — 「省了 / 多了 X」
30 秒：CTA — 「下一步」
```

### Demo 結構（技術版 10 分鐘）
```
30 秒：問題 + 用戶
2 分鐘：架構圖 + 選型理由
3 分鐘：live demo（重點段）
2 分鐘：踩過的 3 個坑
1 分鐘：監控 + 復盤
1 分鐘：未來迭代
30 秒：Q&A intro
```

### Demo 準備 checklist
- [ ] 投影片 < 10 頁（不要 20 頁）
- [ ] 至少在組內 dry run 3 次
- [ ] 每段都有人 backup（demo 翻車那位不講話）
- [ ] 螢幕錄影備份（萬一網路掛）

---

## ⑩ 復盤（W19）

詳見 [06 復盤 + 課後加強路徑](06-retro-and-after.md)。

關鍵：**復盤完才算真正畫上句點**。沒做復盤，這段累積的學習很容易在兩個月後忘光，下次遇到類似情境又會踩同個坑。


---

## 🎯 小作業：寫好 PLAN.md + task.md 第一版

把本章的 10 階段轉成你們組的執行計畫。

- [ ] 用 [template-repo/PLAN.md](template-repo/PLAN.md) 為模板，填好「問題定義 + 系統設計 + Sprint 計畫」三段
- [ ] 用 [template-repo/task.md](template-repo/task.md) 為模板，把初期任務拆成 4-6 個 task
- [ ] 每個 task 都標 owner
- [ ] 各人主擔的角色寫進 PLAN.md「分工」段（4 種角色：Ingest / Pipeline / Analytics / Product）

**交付**：把這兩份檔案 commit + push，repo 連結貼到指定 channel。(暫時不用)

---

下一步：[04 8 情境痛點 × 業界對應地圖 →](04-pain-points-industry-map.md)
