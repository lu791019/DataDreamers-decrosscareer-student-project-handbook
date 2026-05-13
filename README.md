# 學員專題實戰手冊

> **目標**：從 0 到 1 建立「面試作品集」，並且升級成「業界最低標準等級的專案」。
> **作者**：Dex ／ 雲端資料工程師養成班 專題導師
> **對象**：TibaMe 養成班學員

---

學員專題大致可以分成三種樣貌：

| 等級 | 樣貌 | 面試時的結果 |
|---|---|---|
| 作業 | 跑得起 notebook、沒架構圖、demo 是手動 run 一次 | 面試官比較難看到亮點 |
| 作品 | 有敘述、能持續執行、技術棧豐富 | 「不錯，但跟別人差不多」 |
| MVP 最小可行性產品 (demo) | 有架構圖、有歷史紀錄、有監控、有下一步行動、能講為什麼選 A 不選 B | 「我們想了解這個專案」 |

**透過這裡幫你達到第三種等級**

---

## 先了解的 4 件事

1. **Data Pipeline 通用藍圖** — 所有 DE 專案的骨架是同一套，看完就再也不會「不知道從哪開始」
2. **小組 10 階段流程** — 從第一次討論到 demo day 的完整 SOP
3. **協作過程** — 敏捷開發、Git 版本控制、溝通工具、專案管理工具
4. **8 情境完整 walkthrough** — 不是抽象方法論，是 8 種場景能照著走，並加以改造

---

## 手冊閱讀方法

依你目前的狀態，找到適合的閱讀路徑：

| 你的狀態 | 🎯 必讀（先看） | 📖 接著補 | ⏱ 估時 |
|---|---|---|---|
| 🌱 **完全沒用過 GitHub** | [00 GitHub 註冊 SOP](00-github-setup-sop.md) | [03 協作 SOP](03-collaboration-sop.md) | 30 min |
| 🤝 **還沒組好隊 / 不知怎麼啟動** | [02 10 階段流程](02-team-process.md)（① 啟動段） | [07 敏捷與工具選型](07-agile-and-tools.md) | 45 min |
| 🎯 **組好了、正在選題** | [04 痛點 × 業界地圖](04-pain-points-industry-map.md) | [scenarios/](scenarios/) 挑 1-2 個對齊 | 60 min |
| 🏗 **開始實作、不知如何設計** | [01 通用管線藍圖](01-pipeline-blueprint.md) | 對應的 scenario 文件 | 45 min |
| 🛠 **動工中卡關 / 流程亂** | [03 協作 SOP](03-collaboration-sop.md) + [07 敏捷與工具](07-agile-and-tools.md) | [02 10 階段流程](02-team-process.md)（⑥ 衝刺段） | 60 min |
| 🎤 **快到 demo 了** | [06 Demo Day 評分表](06-demo-day-rubric.md) | [05 復盤模板](05-retro-and-after.md)（先寫 sprint retro） | 30 min |
| 📜 **專題完了想升級履歷** | [05 課後加強路徑](05-retro-and-after.md) | 重看 [06 評分表](06-demo-day-rubric.md) self-check | 90 min |
| 👀 **第一次來、想全覽** | 從本 README 看完目錄 → 看 1 部 [學長姐 demo](https://www.youtube.com/playlist?list=PL0seqKy3cp6nYX8aFh9oicSh0Gg4BGhQd) | [02 10 階段流程](02-team-process.md) | 90 min |

> 💡 **不確定該看哪條路徑？** 從第一列開始往下找，遇到第一個「對」的情境就停 —— 那條最適合你現在。

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
- [07 敏捷開發 + 工具選型](07-agile-and-tools.md) — Scrum 節奏 + Discord/Slack/Notion/Trello/Linear 選哪個

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
