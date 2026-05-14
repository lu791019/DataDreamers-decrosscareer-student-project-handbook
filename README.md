# 學員專題實戰手冊

> **目標**：從 0 到 1 建立「面試作品集」，並且升級成「業界最低標準等級的專案」

---

學員專題大致可以分成三種樣貌：

| 等級 | 樣貌 | 面試時的結果 |
|---|---|---|
| 作業 | 跑得起 Jupyter Notebook、但沒架構圖、demo 只能手動執行 | 面試官比較難看到亮點 |
| 作品 | 有敘述、能持續執行、技術棧豐富 | 「跟其他人差別不大」 |
| MVP 最小可行性產品 (demo) | 有架構圖、有歷史紀錄，甚至能有監控和有下一步行動、能講為什麼選擇用 A 而不是選擇 B | 想深入了解專案 |

**透過這裡幫你達到第三種等級**

---

## 先了解的 4 件事

1. **Data Pipeline 通用藍圖** — 所有 DE 專案的骨架是同一套，看完就再也不會「不知道從哪開始」
2. **小組 10 階段流程** — 從第一次討論到 demo day 的完整 SOP
3. **協作過程** — 敏捷開發、Git 版本控制、溝通工具、專案管理工具
4. **8 情境完整 walkthrough** —  8 種場景能照著走，並加以改造

---

## 手冊閱讀方法

依你目前的狀態，找到適合的閱讀路徑：

| 你的狀態 | 🎯 必讀（先看） | 📖 下一步 | 
|---|---|---|
| 🌱 **完全沒用過 GitHub** | [00 GitHub 註冊 SOP](00-github-setup-sop.md) | [05 協作 SOP](05-collaboration-sop.md) | 
| 🤝 **還沒組好隊 / 不知怎麼啟動** | [03 10 階段流程](03-team-process.md)（① 啟動段） | [02 敏捷與工具選型](02-agile-and-tools.md) | 
| 🎯 **組好了、正在選題** | [04 痛點 × 業界地圖](04-pain-points-industry-map.md) | [scenarios/](scenarios/) 挑 1-2 個對齊 | 
| 🏗 **開始實作、不知如何設計** | [01 通用管線藍圖](01-pipeline-blueprint.md) | 對應的 scenario 文件 |
| 🛠 **動工中卡關 / 流程亂** | [05 協作 SOP](05-collaboration-sop.md) + [02 敏捷與工具](02-agile-and-tools.md) | [03 10 階段流程](03-team-process.md)（⑥ 衝刺段） |
| 🎤 **快到 demo 了** | [07 Demo Day 評分表](07-demo-day-rubric.md) | [06 復盤模板](06-retro-and-after.md)（先寫 sprint retro） |
| 📜 **專題完了想升級履歷** | [06 課後加強路徑](06-retro-and-after.md) | 重看 [07 評分表](07-demo-day-rubric.md) self-check |
| 👀 **第一次來、想全覽** | 從本 README 看完目錄 → 看 1 部 [學長姐 demo](https://www.youtube.com/playlist?list=PL0seqKy3cp6nYX8aFh9oicSh0Gg4BGhQd) | [03 10 階段流程](03-team-process.md) |

---

## 目錄

### 📐 專案協作系列（每章對應一週）

| 週 | 章節 | 重點 |
|---|---|---|
| **第 0 週** | [00 GitHub 註冊、開通與 Fork SOP](00-github-setup-sop.md) | GitHub 帳號 + repo 設定 |
| **第 1 週** | [01 通用資料管線藍圖](01-pipeline-blueprint.md) | 六階段骨架 + ETL/ELT + 工具選型決策樹 |
| **第 2 週** | [02 敏捷開發 + 溝通與專案管理工具選型](02-agile-and-tools.md) | Scrum 節奏 + Discord/Slack + Trello/Notion/GitHub Projects |
| **第 3 週** | [03 小組專案 10 階段流程](03-team-process.md) | 啟動 → 復盤的 20 週完整 SOP |
| **第 4 週** | [04 8 情境痛點 × 業界對應地圖](04-pain-points-industry-map.md) | 選題 × 業界職位對應 |

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

### 📚 持續參考（不綁定週次）
- [05 業界協作 SOP](05-collaboration-sop.md) — Git / GitHub / PR / Code Review（實作期天天看）
- [06 復盤 + 課後加強路徑](06-retro-and-after.md) — KPT / 4Ls / 履歷升級 checklist（每 sprint 末用）
- [07 Demo Day 評分表](07-demo-day-rubric.md) — 業界 demo 最低門檻（學期末用）

---

## 過往學長姐 demo

YouTube 公開：

**🔗 [完整 playlist](https://www.youtube.com/playlist?list=PL0seqKy3cp6nYX8aFh9oicSh0Gg4BGhQd)**

**怎麼看才有效**：

- 找清單中有興趣的 1~3 個過去專題觀看
- 回答 3 個問題：
  1. 他們解的是什麼業務問題？
  2. 技術用了哪些？
  3. 我能比他們做得更好的地方是什麼？

---

## 配套課堂材料

這份手冊跟你在課堂上看到的三份簡報是一套，互相補強：

| 階段 | 課堂簡報 | 對應手冊章節 |
|---|---|---|
| 課程開始 | **課程總覽 & DE 介紹** ([PDF](../課程總覽%26DE介紹.pdf)) | README + [04 痛點地圖](04-pain-points-industry-map.md) |
| 前置期 W1-W3 | **期初工作坊：資料解決方案顧問** ([PDF](../期初工作坊.pdf)) | [01 通用管線藍圖](01-pipeline-blueprint.md) + [scenarios/](scenarios/) |
| 實作期 W10-W12 | **期中工作坊：個人 pipeline 實作** ([HTML](../course_project_slides.html)) | [03 10 階段流程](03-team-process.md) + [05 協作 SOP](05-collaboration-sop.md) |

> 💡 **建議閱讀順序**：先看課堂簡報感受全貌，回手冊查細節與作業。

---

## 記住心法

> **「業界專案不是把技術秀出來，是把情境、痛點、解法(最優解和最快解)、遇到的技術問題和如何處理等講清楚。」**

---

## 關於作者

**Dex** — 資料工程教練、自媒體經營者、個人品牌 DayDreamDex 塵世哲學。

過去 10 年從 半導體QA 跨到資料工程、軟體開發 和 AI開發，現在則是教學講師與諮詢業師。多重身份包含：
- **TibaMe 雲端資料工程師養成班** 專題業師
- **DayDreamDex** 主理人 — Dex 的塵世哲學品牌
- **我與經驗值（IandExp）** 電子報主筆 — 寫給轉職者 / DE / 求知者的雙週信
- **沒走歪的才奇怪** Podcast 主持人 — 跟走過彎路的人聊「彎路怎麼變捷徑」

讓我們一起在轉折點上慢慢前行

如果這份手冊對你有用，最大的回饋是讓我知道：你做到哪了、卡在哪、需要什麼

### 關於 Dex

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

### 看完手冊後可以怎麼做

1. **透過電子報或其他方式與我討論**
2. **把這份手冊分享給也在轉職的朋友** 
3. **訂閱「我與經驗值」電子報** — 雙週收到 DE / 職涯 / 真實案例

---

## License
- ✅ 自由閱讀、分享、改編
- ✅ 商業用途請先聯繫
- ⚠️ 改編後需註明原作者並用相同授權

GitHub Repo: [github.com/lu791019/tibame-student-project-handbook](https://github.com/lu791019/tibame-student-project-handbook)（star ⭐ 一下方便日後找回）
