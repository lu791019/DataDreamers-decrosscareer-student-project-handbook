# 學員專題實戰手冊

> **目的**：把「課堂作品集」升級成「業界最低標準的 demo 等級專案」。
> 你跟一般學員的差距不在技術，而在**流程、協作、復盤、表達**。這份手冊把這四件事補齊。

**作者**：Dex（盧冠宏）／TibaMe 雲端資料工程師養成班 教練
**對象**：TibaMe 養成班學員、自學者轉職組、想做出能放履歷的 DE 專題的人
**版本**：v1.0（2026-05-13）

---

## 為什麼需要這本手冊？

學員專題常見三種樣貌：

| 等級 | 樣貌 | 在面試時的命運 |
|---|---|---|
| ❌ 學作業 | 跑得起 notebook、沒有架構圖、commit 訊息全是「update」、README 一句話、demo 是手動 run 一次 | 面試官 30 秒看完就放下 |
| 🟡 學作品 | 有 README、能跑、技術棧多 | 「噢這也算啦」 |
| ✅ 業界 demo | 有架構圖、有 PR 紀錄、有 retro、有監控、能講為什麼選 A 不選 B | 「來聊聊你這個專案」 |

**這份手冊的承諾**：照著做完，你的專案會落在 ✅。

---

## 你會學到的 4 件事

1. **資料管線通用藍圖** — 所有 DE 專案的骨架是同一套，看完就再也不會「不知道從哪開始」
2. **小組 10 階段流程** — 從第一次討論到 demo day 的完整 SOP
3. **業界協作 artifact** — Git / PR / Issue / Code Review / Retro 全套樣板可以直接套用
4. **8 情境完整 walkthrough** — 不是抽象方法論，是 8 個真實業界場景照著走一遍

---

## 這份手冊怎麼讀？

```
你在哪個階段          → 讀哪幾份
─────────────────────────────────
還沒組好隊            → README → 02 → 06 評分標準
組好了選題中          → 04 痛點地圖 → scenarios/* 挑一個對齊
動工中卡關            → 01 藍圖 + 03 SOP
快 demo 了            → 06 評分標準 + 05 復盤模板
專案結束想升級履歷    → 05 課後加強路徑
```

---

## 目錄

### 🚀 開始之前（完全新手）
- [00 GitHub 註冊、開通與 Fork SOP](00-github-setup-sop.md) — 沒用過 GitHub？30 分鐘從零到能 push

### 📐 通用方法論
- [01 通用資料管線藍圖](01-pipeline-blueprint.md) — 6 階段骨架 + 工具選型決策樹
- [02 小組專案 10 階段流程](02-team-process.md) — 啟動 → 復盤的完整 SOP
- [03 業界協作 SOP](03-collaboration-sop.md) — Git / GitHub / PR / Code Review 全套
- [04 8 情境痛點 × 業界對應地圖](04-pain-points-industry-map.md) — 每題對應哪些真實職位
- [05 復盤 + 課後加強路徑](05-retro-and-after.md) — KPT / 4Ls / 履歷升級 checklist
- [06 Demo Day 評分表](06-demo-day-rubric.md) — 業界 demo 最低門檻

### 🎯 8 情境完整 walkthrough
| # | 情境 | 對應產業 | 過往作品參考 |
|---|---|---|---|
| 1 | [餐飲連鎖 POS 庫存優化](scenarios/scenario-1-restaurant-pos.md) | 餐飲 / 零售 | 美味餐廳隨拾取、食喪地圖、找咖小幫手 |
| 2 | [B2C 電商競品比價](scenarios/scenario-2-ecommerce.md) | 電商 | 水果價格預測 |
| 3 | [數位金融客訴效率](scenarios/scenario-3-fintech.md) | 銀行 / FinTech | 反詐騙 LINE Bot、打造自己的 ETF |
| 4 | [音樂串流推薦優化](scenarios/scenario-4-music.md) | 媒體 / 串流 | KKBOX&Spotify 比較、SteamTrend |
| 5 | [叫車服務交通熱點](scenarios/scenario-5-ride.md) | 交通 / 物流 | 國道車流 LSTM、國旅推薦 |
| 6 | [求職媒合職缺趨勢](scenarios/scenario-6-recruit.md) | HR Tech | 求職 360°、求職求值 |
| 7 | [媒體業新聞輿情](scenarios/scenario-7-news.md) | 媒體 / 行銷 | 社群輿情、夜市水軍王、巴哈姆特輿情、遊戲輿情 |
| 8 | [不動產房價趨勢](scenarios/scenario-8-realestate.md) | 不動產 / GIS | 房價走勢密碼、六都寵物便利度 |

### 🛠 GitHub Skeleton（學員 fork 用）
- [template-repo/](template-repo/) — 開好的 repo 範本，含 README / PLAN / task / PR template / CI workflow

---

## 22 部過往學長姐 demo（你的對標）

整個 TibaMe 養成班 TIR102 ~ TJR104 共 22 部專題 demo，YouTube 公開：

**🔗 [完整 playlist](https://www.youtube.com/playlist?list=PL0seqKy3cp6nYX8aFh9oicSh0Gg4BGhQd)**（建議在開始選題前先看 3-5 部）

**怎麼看才有效**：
1. 先看一部完整（20-30 分鐘）感受節奏
2. 看 3 部不同主題、只看 demo 段（架構圖 + 流程 + 結果）
3. 每看一部回答 3 個問題：他們解的是什麼業務問題？技術棧怎麼選的？我能比他們做得更好的地方是什麼？

---

## 心法（一句話）

> **「業界專案不是把技術秀出來，是把問題講清楚。」**
> ── Dex

剩下的細節，去看 02 階段流程。

---

## 關於作者

**Dex（盧冠宏）** — 資料工程教練、自媒體經營者、塵世哲學家。

過去 10 年從 BD 跨到工程、再跨到教學與內容創作。現在的身分是：
- **TibaMe 雲端資料工程師養成班** 教練（4 梯次 / 100+ 學員）
- **DayDreamDex** 主理人 — Dex 的塵世哲學品牌
- **我與經驗值（IandExp）** 電子報主筆 — 寫給轉職者 / DE / 求知者的雙週信
- **沒走歪的才奇怪** Podcast 主持人 — 跟走過彎路的人聊「彎路怎麼變捷徑」

我不是「我教你」，是「我們一起在轉折點上慢慢走」。

如果這份手冊對你有用，最大的回饋是讓我知道：你做到哪了、卡在哪、需要什麼。

### 找到 Dex

| 平台 | 用途 | 連結 |
|---|---|---|
| 📧 **電子報（主力）** | 雙週寄一封：DE / AI / 職涯 / 轉職實戰 | [iandexp.kit.com](https://iandexp.kit.com/e0cd61d37a) |
| 📝 Substack | 電子報備援平台 | [daydreamdex.substack.com](https://daydreamdex.substack.com/) |
| 🧵 Threads | 日常碎念 + 短觀察 | [@daydreamdex](https://www.threads.com/@daydreamdex) |
| 📸 Instagram | 視覺化短內容 | [@daydreamdex](https://www.instagram.com/daydreamdex/) |
| 📘 Facebook | 長文 + 社群 | [Dex 的 FB](https://www.facebook.com/profile.php?id=61560603174482) |
| 🌐 Blog | 長文與深度文章 | [daydreamdex.com](https://daydreamdex.com/) |
| 🎙 Podcast (Spotify) | 沒走歪的才奇怪 | [Spotify 直連](https://open.spotify.com/show/2qV49EUjFOcJIqkUjwmu2T) |
| 📺 YouTube | 教學影片 + Podcast 影音版 | [@WhySoStraight](https://www.youtube.com/@WhySoStraight) |
| 🔗 一站式 | 所有連結 | [portaly.cc/daydreamdex](https://portaly.cc/daydreamdex) |

### 用完手冊之後

1. **寫一段心得寄給我**（電子報回信即可）— 我會回
2. **把這份手冊分享給也在轉職的朋友** — 知識交給需要的人才有意義
3. **訂閱「我與經驗值」** — 雙週收到 DE / 職涯 / 真實案例
4. **加入 [Threads](https://www.threads.com/@daydreamdex) 看日常**

---

## License

本手冊以 **CC BY-NC-SA 4.0** 授權：
- ✅ 自由閱讀、分享、改編
- ✅ 商業用途請先聯繫
- ⚠️ 改編後需註明原作者並用相同授權

GitHub Repo: [github.com/lu791019/tibame-student-project-handbook](https://github.com/lu791019/tibame-student-project-handbook)（star ⭐ 一下方便日後找回）
