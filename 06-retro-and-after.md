# 06 復盤 + 課後加強路徑

> 復盤是把「我做了一個專題」轉成「我學到了 X」的關鍵動作。沒做的話，過了兩個月你會發現自己只記得「做過」，但講不出來具體學到什麼。

---

## Sprint Retro（每週做一次）

### KPT 模板（最常用，20-30 分鐘）

```markdown
# Sprint N Retro - 2026-MM-DD

## Keep（繼續做）
- 每天 standup 維持得不錯，沒人神隱
- 用 PR template 後 review 速度變快

## Problem（要解決）
- Airflow 排程在週末停了沒人發現 → 缺監控
- 三個人同時改 schema 出 conflict

## Try（下週試試）
- 加 GitHub Actions 每天跑健康檢查 + LINE 通知
- Schema 改動必須先開 issue 討論再動工
```

### 4Ls 模板（適合大里程碑 / final retro）

```markdown
## Liked（喜歡的）
## Learned（學到的）
## Lacked（不足的）
## Longed for（希望有的）
```

### Sailboat 模板（適合需要視覺化）

```
🏝 目標：穩定的每日資料更新

⬆️ 風（推進的力量）：
  - Airflow 自動排程
  - 組員技能互補

⚓ 錨（拖累的力量）：
  - 沒人做 documentation
  - Code review 卡 2 天

🦈 鯊魚（風險）：
  - 雲端額度快用完
  - 期末週兩個人有別的考試

🪨 暗礁（過去的坑）：
  - 第 3 週浪費 2 天設定 docker 環境
```

---

## Final Retro（專題結束後 1 週做）

不是 sprint retro 的延伸，是更深的反思。建議組內每人先寫，再合併。

### 個人 final retro 模板

```markdown
# 我的專題復盤 - {你的名字}

## 1. 我學到的 3 件最有價值的事
（不要寫工具名 — 寫思維 / 流程 / 心法）
1.
2.
3.

## 2. 我做得最好的 1 件事

## 3. 如果重來，我會改的 3 件事
1.
2.
3.

## 4. 我下次想加強的技能（具體、可量化）
- [ ] 在 X 時間前學會 Y
- [ ] 加入某社群 / 看完某書 / 完成某課程

## 5. 給組員的 feedback（每人 1 條）
- @組員A：你的 X 很強 / 你可以加強 Y
- ...

## 6. 給未來自己的話
（一封寫給「3 個月後的自己」的信）
```

### 小組 final retro

集合所有人個人 retro 後一起做：
1. **共識** — 我們認同的 3 件事
2. **分歧** — 我們看法不同的事（不要試圖統一，保留多元視角）
3. **總教訓** — 一句話送給下一屆學員

---

## 課後加強路徑

專題結束不是終點。這時候你會發現「能講」和「能拓展」是兩件事。

### 第 1 個月：把專題變成「履歷代表作」

#### Week 1：repo 重整
- [ ] README 重寫（用 [03 SOP](04-collaboration-sop.md) 的元素清單）
- [ ] 加上 GIF demo（用 [Kap](https://getkap.co/) 錄 20 秒）
- [ ] 把 commit message 全部審一次，太爛的 squash
- [ ] 加 LICENSE（MIT 最簡單）

#### Week 2：架構圖補齊
- [ ] 用 draw.io 重畫一張高品質架構圖
- [ ] 補 `docs/architecture-decisions.md`：為什麼選 A 不選 B（ADR 格式）
- [ ] 補 `docs/lessons-learned.md`：踩過的 5 個坑

#### Week 3：寫 1 篇 blog post
- 題目建議：「我做 X 專題踩過的 N 個坑」
- 發 Medium / DEV / 自己的 Blog
- 在 LinkedIn / Threads 分享

#### Week 4：影片化
- 錄一支 5-10 分鐘 demo 影片（用業務版講稿）
- 上 YouTube unlisted（不公開但可分享連結）
- 履歷 / LinkedIn 內嵌

---

### 第 2-3 個月：技術深化（選 1-2 個方向）

| 方向 | 推薦資源 | 目標 |
|---|---|---|
| **dbt + BigQuery 維度建模** | dbt fundamentals course | 把你的專案 Process 層重寫成 dbt |
| **Streaming（Kafka / Pub/Sub）** | Confluent dev courses | 加一條即時管線 |
| **MLOps / ML pipeline** | MLOps Zoomcamp（DataTalksClub）| 把模型 production 化 |
| **Cloud 認證** | GCP Pro Data Engineer / AWS DA | 履歷加分 |
| **LLM Engineering** | DeepLearning.AI short courses | 加 RAG / Agent 在你的專案 |

---

### 第 4-6 個月：拓展應用

選 1 個方向：

#### A. 把專題擴展成 SaaS
- 找 5 個朋友當試用
- 收 $99 一年（驗證有沒有人付）
- 學商業面（不是技術面）

#### B. Open source 化
- 把核心部分抽成 package
- 上 PyPI
- 寫貢獻 guide

#### C. 加入 OSS 社群
- 從 Apache Airflow / dbt / Great Expectations 挑一個
- 從 「good first issue」開始
- 半年內成為 contributor

---

## 「面試怎麼講」3 種版本

### 5 秒版（電梯 / 自介）
> 「我做了一個 [情境]，從 [來源] 抓資料，每天自動跑出 [產出]。」

例：「我做了一個音樂推薦系統，從 Spotify API 抓 50 萬筆聽歌紀錄，每天自動跑出個人化新歌清單。」

### 30 秒版（履歷自介段、HR phone screen）
```
[痛點 5 秒] 現在 X 要花 Y 時間/錢
[方案 10 秒] 我做了一個 [系統]，做了 A、B、C 三件事
[影響 10 秒] 結果是 D 提升 X%，組員 N 個人花了 N 個月
[技術棧 5 秒] 用了 X / Y / Z
```

### 5 分鐘版（技術面深聊）
跟著 [02 階段流程的 demo 結構](03-team-process.md#demo-結構技術版-10-分鐘)走，但減掉前後段，留：
1. **問題 30 秒**
2. **架構 + 選型 90 秒**：為什麼選 A 不選 B
3. **demo 90 秒**
4. **踩過的 2 個坑 60 秒**：技術面試官最愛
5. **未來 30 秒**

---

## 履歷怎麼放

### 範例（DE 履歷的「專案」欄位）

```
🚀 餐飲多門市庫存優化儀表板 (2026/03 - 2026/05)
   GitHub: github.com/dex/restaurant-pos-pipeline  |  Live demo: ...

   - 主導 4 人組「資料工程養成班」期末專題，從 Kaggle Restaurant Orders +
     UCI Retail 兩個資料源建立端到端 pipeline
   - 架構：Python ingest → MySQL → Airflow（每日 6am）→ Streamlit
   - 實作補貨建議演算法，依據 7 日滑動平均 + 銷售趨勢，預測庫存到底日
   - 加入 dbt tests + LINE notify，pipeline 失敗 5 分鐘內收到通知
   - 完整 PR review 流程、文件齊全、組員 30 個 PR 全部 reviewed merged
```

✅ 動詞開頭 ✅ 有數字 ✅ 有具體技術 ✅ 連結可驗證

❌ 不要寫：「使用 Python 完成了一個專案」「學習了很多」「跟組員合作」

---

## 你 6 個月後的樣子

如果照這份路徑走，半年後你會：

- ✅ 有 1 個能放履歷的高品質 repo
- ✅ 有 1 篇技術 blog post
- ✅ 有 1 支 demo 影片
- ✅ 在 1-2 個技術方向有更深的內功
- ✅ 在 1 個 OSS / SaaS / 社群有實際參與
- ✅ 面試講你的專案能輕鬆切換 5 秒 / 30 秒 / 5 分鐘 3 種版本

**這是業界 senior 看你的差距 — 不是工具，是這份累積。**

---

## 🎯 小作業：寫第一份 sprint retro

Sprint 1 結束的週日，全組坐下來做。

- [ ] 用 KPT 模板（Keep / Problem / Try）寫
- [ ] Keep / Problem / Try 各至少 2 條
- [ ] 每條 Try 都對應一個下週的 action item + assignee
- [ ] 存到 repo 的 `docs/retro/sprint-1.md` commit
- [ ] 把上週 Try 的 action items 抄到下一份 sprint plan

**交付**：PR 連結貼到指定 channel。

> 💡 寫「都很好」「都很順」= 沒做 retro，這時候請組長重開一次討論。誠實的 retro 才有用。

---

下一步：[07 Demo Day 評分表 →](07-demo-day-rubric.md)
