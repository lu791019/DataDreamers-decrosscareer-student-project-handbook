# 02 小組專案 10 階段流程

> 這是把 8 週小組專案做完的完整 SOP。每階段都有：**目標 / 產出物 / 時間預算 / 卡關處方 / 教練視角**。

---

## 全景圖

```
週次   階段                 產出物                          重點
─────────────────────────────────────────────────────────────────
W0    ① 啟動               組員契約 / 題目共識             先選人後選題
W1    ② Discovery          用戶 / 業務 / 痛點 / 資料清單   多走一步
W2    ③ 設計               架構圖 / ER 圖 / API 契約       先紙上後上線
W2    ④ 分工               角色矩陣 / 認領表                按強項不按平均
W3    ⑤ 環境               GitHub repo / branch 規範        第一週就立規矩
W3-6  ⑥ 衝刺（3 個 sprint）daily standup / weekly review    跑得起來最重要
W6    ⑦ 整合               API 契約對齊 / e2e 測試          整合先於優化
W7    ⑧ 上線               部署 / 監控 / 文件                能讓別人用到
W7    ⑨ Demo               技術版 + 業務版兩種                練到能背
W8    ⑩ 復盤               retro / 履歷升級                  收尾才是 alpha
```

---

## ① 啟動（W0，約 4 小時）

### 目標
**確定組員、選定題目、簽組員契約**。

### 產出物
- `team-charter.md`：組員名單 / 強項 / 弱項 / 時區 / 每週可投入時數
- `topic-decision.md`：選了哪個情境、為什麼選、目標用戶
- 一個共用通訊工具（Slack / Discord / LINE 群）

### 時間預算
- 1.5 hr：互相認識 + 強項盤點
- 1.5 hr：8 情境選題
- 1 hr：寫契約 + 開群

### 卡關處方

| 卡關 | 處方 |
|---|---|
| 都選最熱門題目 | 看 04 痛點地圖 — 哪題對「你過去職涯」最有故事 |
| 大家都想當 lead | 用 RACI 分工，沒有「lead」只有 4 種角色 |
| 有人不想表態 | 用 dot voting 投票，每人 3 票 |

### 教練視角
- **選題比技術重要**：選一個「面試時你能講 5 分鐘為什麼選」的題目，遠比「最潮的題目」有用。
- **不要為了平均而平均**：4 個人都「平均寫 25%」會做出爛專案。讓強項極大化。

---

## ② Discovery（W1，約 8 小時）

### 目標
**搞清楚：誰在用、為什麼用、痛在哪、資料怎麼來**。

### 產出物
- `docs/user-persona.md`：1-2 個具體 persona（不是「年輕人」這種廢話）
- `docs/pain-points.md`：3-5 個具體痛點（要可量化）
- `docs/data-inventory.md`：所有可能資料來源清單（含取得難度評估）

### 時間預算
- 3 hr：訪談 / 看現有報告 / 蒐集二手資料
- 2 hr：寫 persona + pain points
- 3 hr：盤點資料來源 + 跑 1-2 個 API / 爬蟲 POC

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
| 找不到資料 | 看 01 藍圖 Source 段 — 90% 用 API + 爬蟲解 |
| 痛點寫得很抽象 | 加數字：「每天平均花 X 分鐘做 Y」 |

---

## ③ 設計（W2，約 12 小時）

### 目標
**畫出系統長什麼樣 — 在寫一行 code 之前**。

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
| 大家畫的不一樣 | 用 Mermaid + PR，強制收斂 |

---

## ④ 分工（W2，約 2 小時）

### 目標
**讓每個人有清楚的 ownership，但沒人是孤島**。

### 4 種角色（不是 1 種）

| 角色 | 職責 | 適合的人 |
|---|---|---|
| **Data Ingest Owner** | 爬蟲 / API / 資料品質 | 細心、抗錯耐性高 |
| **Pipeline Owner** | Airflow / Docker / 排程 | 喜歡自動化 |
| **Analytics Owner** | SQL / pandas / 模型 | 數理直覺好 |
| **Product Owner** | Streamlit / API / UX | 會講故事、會 demo |

> **每人主擔 1 個角色 + 副擔 1 個角色**，不是完全分割。

### RACI 矩陣（範例）

| 任務 | 阿凱 | 小美 | 大華 | 小婷 |
|---|---|---|---|---|
| 爬蟲開發 | **R** | C | A | I |
| Airflow 排程 | C | **R** | I | A |
| 分析模型 | I | A | **R** | C |
| Streamlit | A | I | C | **R** |
| Code Review | C | C | C | C |

> R = Responsible（動手）／ A = Accountable（負責）／ C = Consulted（要問）／ I = Informed（要告知）

### 卡關處方

| 卡關 | 處方 |
|---|---|
| 有人攬太多 | 強制每人最多 1 個 R |
| 沒人想做 Product Owner | 那位通常是面試最吃香的 — 點名 |
| 有人沒事做 | 沒事做的人去寫 Code Review + 文件 |

---

## ⑤ 環境（W3，第一天，約 4 小時）

### 目標
**規矩立在前面 — 之後就不用吵架**。

### 產出物
- GitHub repo 建好（用 [template-repo/](template-repo/) 直接 fork）
- Branch 規範：`main` / `develop` / `feature/*` / `fix/*`
- 第一個 PR 跑通 CI
- README / PLAN / task.md 三件套

### 細節展開請見 [03 業界協作 SOP](03-collaboration-sop.md)

---

## ⑥ 衝刺（W3-W6，3 個 sprint × 1 週）

### 節奏
```
週一  sprint planning (1 hr)     決定本週做什麼
週一-五  daily standup (10 min)    我做什麼 / 卡什麼 / 需要誰幫
週五  sprint review (1 hr)        demo 給組內看
週日  sprint retro (30 min)       什麼 ok 什麼不行
```

### Sprint 1（W3）：跑通最小可行 pipeline
- 目標：**端到端跑得起一遍**，醜沒關係
- 完成度：Source → Storage → 一個結果（哪怕是 print）
- 反例：花一週把爬蟲調到完美 → 你 demo 沒得展

### Sprint 2（W4-5）：擴充 + 自動化
- 目標：加排程 + 加更多資料源 + 加分析
- 完成度：能每天自動跑、有 dashboard 雛形

### Sprint 3（W6）：打磨 + 監控
- 目標：UI 順、有監控、文件齊
- 完成度：別人能自己跑起來

### 卡關處方

| 卡關 | 處方 |
|---|---|
| 進度落後 | **砍 scope** 不是熬夜 — 砍掉 next-to-have |
| 有人神隱 | 馬上 escalate 給教練，不要拖 |
| 一直 refactor | sprint 中禁 refactor，sprint review 才討論 |

---

## ⑦ 整合（W6-W7，約 8 小時）

### 目標
**把 4 個人的 code 串成一個 pipeline**。

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

## ⑧ 上線（W7，約 6 小時）

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

## ⑨ Demo（W7-W8）

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

## ⑩ 復盤（W8，2 小時）

詳見 [05 復盤 + 課後加強路徑](05-retro-and-after.md)。

關鍵：**復盤完才算真正畫上句點**。沒做復盤，這 8 週累積的學習很容易在兩個月後忘光，下次遇到類似情境又會踩同個坑。

---

## 時間預算總表

| 階段 | 工時 / 人 | 週次 |
|---|---|---|
| ① 啟動 | 4 hr | W0 |
| ② Discovery | 8 hr | W1 |
| ③ 設計 | 12 hr | W2 |
| ④ 分工 | 2 hr | W2 |
| ⑤ 環境 | 4 hr | W3 初 |
| ⑥ 衝刺（3 sprint）| 30-40 hr | W3-W6 |
| ⑦ 整合 | 8 hr | W6-W7 |
| ⑧ 上線 | 6 hr | W7 |
| ⑨ Demo | 6 hr | W7-W8 |
| ⑩ 復盤 | 2 hr | W8 |
| **總計** | **~85 hr / 人** | 8 週 |

> 換算：每週約 10-12 小時 — 跟業界小型專案類似節奏。

---

下一步：[03 業界協作 SOP →](03-collaboration-sop.md)
