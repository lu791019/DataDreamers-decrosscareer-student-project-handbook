# 專案協作第 2 週 ｜ 02 敏捷開發 + 溝通與專案管理工具選型

> 流程跑得順、訊息傳得清楚、卡關有人接 —— 這三件事決定整個學期能不能順利走完。
> 這篇幫你把「該怎麼跑」和「該用什麼工具」一次想清楚。

---

## Part 1：敏捷開發 — 小組專案的最佳節奏

### 為什麼是敏捷開發？

學員專案時間有限、組員幾個、需求會變、不會做完美 —— 這正是敏捷被設計來解決的場景。

> 敏捷不是「速度快」，是「願意接受『我們一開始想的不完全對』，然後快速調整」。

直接照搬企業的 Scrum 方法會太笨重。下面是給「小組專題」剪裁過的版本 (模擬 Scrum 的簡化方法，關於Scrum正式做法補充在最後)

---

### 為什麼選 Scrumban（不選完整 Scrum 或純 Kanban）

業界有兩大主流：

| 學派 | 一句話特色 | 對小組的問題 |
|---|---|---|
| **Scrum** | 用 sprint 把時間切成等長格子，含 5 個 ceremonies | 5 個 ceremonies 對 3 人組太重，開會時間 > 寫 code 時間 |
| **Kanban** | 用看板視覺化、WIP limit 限制同時做的事 | 沒有節奏感，學員容易拖延 |

**Scrumban = 兩者折衷**：保留 Kanban 看板 + 採 Scrum 的雙週節奏 + 只做最關鍵的兩個 ceremonies。

> 業界小團隊（新創 / 3-10 人）最常用 Scrumban

---

### Scrumban 三大支柱

```
1. 看板 + WIP limit       任務狀態視覺化，限制同時做的事（每人最多 3 個 in-progress）
2. Sprint Planning        每 1 週開一次，決定這週要做什麼
3. Sprint Review          每 1 週開一次，跟組內確認想法或功能
```

**輔助**：
- 異步 Daily Check-in（溝通通句進行文字討論）
- final retro（只在學期末做，看 [06 章](06-retro-and-after.md)）

**不用做的**：
- ❌ Sprint Retro（反省會議是不斷迭代和優化的關鍵，但課程中每週去做會容易疲乏；改成學期末做一次深度 final retro）
- ❌ Velocity / Story Points（本來跑敏捷有所謂的計點制方式，每個人都有被分配的點數量要完成，但課程中我們有意識地持續「推進」就好）

---

### 看板長怎樣

```
📥 Backlog        🎯 This Sprint    🚧 In Progress    👀 Done        ✅ Done
還沒排程           本 2 週要做       進行中（限 2/人）   等 Review 或確認     已完成
─────────         ─────────         ─────────         ─────────        ─────────
T-001             T-005             T-002 (Alice)     T-006 (Bob)      T-001
T-008             T-006             T-003 (Bob)                         T-004
T-009             T-007             T-007 (Carol)
...               T-008
                  T-009
```

**WIP limit 規則**：每人 In Progress 最多 3 張卡。每張卡片要能在半天完成，**超過要先做完一張才能新開**。
(這就是 Kanban 精髓 —— 強迫聚焦、暴露瓶頸)

---

### Sprint Planning 怎麼做（每 1 週一次，每次限定 45-60 分鐘，嚴格計時）

**前置**：看板 Backlog 有待認領任務寫好。

```
00-10 min   回顧上週進度（看板上 Done 欄、本期該完成沒完成的卡）
10-30 min   挑本週要做的任務 → 從 Backlog 拖到 This Sprint
            ── 每張卡有：owner、估時、acceptance criteria
30-50 min   風險討論（哪裏會卡、可能有什麼意外、可能誰本週比較忙碌、API 額度等…）
50-60 min   結論 + 看板更新
```

**估時用 size 區分**：
- **S** = 半天能做完
- **M** = 1-2 天
- 超過 M 就要把討論任務或分配，將任務拆成更細或是有人能協助分工

---

### 異步 Daily Check-in

不開會！每天上午 09:30 在 團隊溝通工具 的三句重點：

```
昨天：我做了 X
今天：我打算做 Y
卡：我卡在 Z，需要如何幫忙
```

**如果沒卡，也要明確說「沒卡」** —— 不然不知道是真的順還是不想講。

> 開 daily 會議是學員小組最容易疲乏的地方。文字版省時間、有紀錄、可以慢慢回。

---

### Sprint Review — 跟組內看「真的能用嗎」（每 2 週一次，45-60 分鐘）

**Review 的真正目的**：
- 對「自己人」demo，看「東西是不是真的能用」
- 收 feedback 給下 sprint
- 教練 / 同學在這時候給意見成本最低

**結構（60 分鐘）**：
```
0-15 min   product owner(組長) 講「這 2 週做了什麼」
15-35 min  確認、測試功能的效果(小demo)
35-50 min  Q&A + 反饋
50-60 min  決定哪些反饋進下 sprint backlog
```

---

### 進度追蹤 — 用「點數預算 + 完成率」（輕量量化）

不用企業那種 story point 估算，但也不靠感覺。3 步驟就可以量化：

#### Step 1 — 估時轉成點數

每張卡片在 Sprint Planning 時標 size，對應一個點數：

| Size | 工時 | 點數 |
|---|---|---|
| **S** | 半天能做完 | **1** |
| **M** | 1-2 天 | **2** |
| **L** | 3-4 天（超過要拆） | **4** |

#### Step 2 — 算 Sprint 預算

```
Sprint 預算 = This Sprint 欄所有卡片的點數加總
```

例：本期 8 張卡 = 3S + 4M + 1L → 預算 3×1 + 4×2 + 1×4 = **15 點**

> 第一個 sprint 憑直覺挑「應該做得完」的量；做完之後，下個 sprint 就有「我們組真實的負荷」作參考。

#### Step 3 — Sprint 結束算「完成率」

```
完成率 = 完成的點數 / 預算點數 × 100%
```

連續 3 個 sprint 後，你會看到組裡真實的 velocity：

| Sprint | 預算 | 完成 | 完成率 |
|---|---|---|---|
| Sprint 1 | 15 | 9 | 60% |
| Sprint 2 | 12 | 10 | 83% |
| Sprint 3 | 11 | 10 | 91% |

**判讀**：
- 完成率 **≥ 80%** → 健康，下 sprint 可以稍微加量
- 完成率 **60-80%** → 還行，下 sprint 維持預算
- 完成率 **< 60%** → 嚴重，下 sprint 砍預算 + 看看是不是估算太樂觀

---

### 砍 scope 的藝術 — 用優先級 + 明確 trigger

學員專案最大的死因不是「做不出來」，是「沒有勇氣砍」。
靠規則，不靠勇氣。

#### 每張卡開始就標 4 級優先級

| 優先級 | 意思 | demo 沒這個會怎樣 |
|---|---|---|
| **P0 — must have** | demo 一定要展、絕不能砍 | demo 沒辦法走完 |
| **P1 — should have** | demo 沒這個會被嫌「不完整」| demo 能跑但被問會卡 |
| **P2 — nice to have** | 加分項，先放著 | demo 不影響 |
| **P3 — delight** | 想做但純為自己爽 | 完全不影響 |

> 規則：**P0 不准砍**。砍順序：P3 → P2 → P1。Sprint Planning 排卡片時，P0 + P1 加起來不該超過預算的 70%。

#### 明確的「該砍了」trigger

| 觸發條件 | 動作 |
|---|---|
| Sprint 過半（W4 / W7 / W10... 第 4 天），剩餘點數 > 預算 60% | 開砍 P3，必要時砍 P2 |
| 同一張 P0 卡片 in-progress > 2 天 | 拉教練 + 把卡拆小 |
| 連續 2 個 sprint 完成率 < 60% | 下 sprint 直接砍 30% scope（不用討論） |
| Demo 前 1 週 P1 還沒做完 | 全部 P2 / P3 砍掉，把資源集中到 P1 |

> 💡 **砍 scope 不是失敗 — 是聰明**。業界 PM 一年砍幾十次。重要的是 P0 必有、按時 demo。

---

## Part 2：溝通工具選型

「我們組討論在哪？」這件事如果沒在第一週決定，整個 sprint 都會混亂。

### 工具地圖

```
即時 / 同步 ───────────────────────── 非同步 / 紀錄
     │                                      │
   LINE     Discord      Slack      Notion / GitHub
   群組     社群型        企業型     文件型
     │        │            │              │
     │        │            ▼              │
     │        │       適合多 channel       │
     ▼        ▼       適合 thread          ▼
   速度快   速度快+      品質高           品質高
   品質低   有 channel   $$              速度慢
```

### 學員小組的推薦組合

#### 推薦 1：Discord + Notion/Trello + GitHub（最多人用）

| 工具 | 用途 | 為什麼 |
|---|---|---|
| **Discord** | daily standup / 即時討論 / voice call | 免費 / 多 channel / 整合機器人方便 |
| **Notion/Trello** | 會議紀錄 / 文件 / PLAN 中間版 | 共編好、好搜尋 |
| **GitHub Issues** | task / bug / 決策紀錄 | 跟程式碼放一起、追溯方便 |

#### 推薦 2：LINE + Google Drive + GitHub

| 工具 | 用途 | 為什麼 |
|---|---|---|
| **LINE 群組** | 即時討論 / 提醒 | 大家本來就有、學習曲線零 |
| **Google Docs / Sheets** | 共編文件 | 老一輩 / 業界都會用 |
| **GitHub Issues** | task | 同上 |

---

### Discord vs Slack vs LINE 三個直球比較

| 維度 | Discord | Slack | LINE 群 |
|---|---|---|---|
| **學習曲線** | 中 | 中 | 零 |
| **多 channel** | ✅ | ✅ | ❌ |
| **thread 討論** | ✅ | ✅ | ❌ |
| **語音會議** | ✅ 內建 | 要 huddle | 通話 |
| **整合機器人** | ✅ 超多 | ✅ 但要付費 | 有限 |
| **保留歷史** | ✅ | 免費版 90 天 | ✅ |
| **業界用得多** | 較少 | 多 | 在地小公司 |
| **檔案傳輸** | ✅ 大檔 OK | 限額 | 限額 |
| **費用** | 免費 | 免費 / 付費 | 免費 |

> 建議：專題用 **Discord** —— 學習曲線適中、機器人整合方便、學完還能用在其他社群活動。

---

### Channel 設計（Discord / Slack 共用）

開好下面這幾個 channel，溝通密度提升 50%：

```
#announce        重大公告（pin 用、不灌水）
#standup         daily standup（每天一篇）
#general         輕鬆閒聊、迷因、加油
#ingest          ingest 模組討論
#pipeline        pipeline / airflow
#analytics       分析 / 模型
#serve           前端 / API
#review          PR review 通知 + 討論
#alerts          Sentry / monitoring 自動通知
#help            卡關喊救命專用
#decisions       做了什麼決策、為什麼（重要的）
#standup-from-bot  GitHub bot 自動通知（PR / Issue）
```
---

### Notification 設定（不被噪音淹）

- **#announce / #alerts**：全員開通知（重要）
- **module channels**：只 owner 開即時、其他人 daily summary
- **#general**：關通知，自己想看再看
- **DM**：要小心 —— 業界討論盡量公開到 channel，避免「只有我跟你知道」

---

## Part 3：專案管理工具選型

這是「task 放哪裡 / sprint 怎麼追」的選型。

### 4 種主流工具直球比較

| 工具 | 學習曲線 | 適合規模 | 強項 | 弱項 | 費用 |
|---|---|---|---|---|---|
| **Trello** | ⭐ 最低 | 1-5 人 | 直覺 / 看板拖拉 | sprint 觀念弱、報表少 | 免費 / 個人版 OK |
| **Notion** | ⭐⭐ | 1-10 人 | 跟文件整合好 | Database 慢、view 切換麻煩 | 免費 / Pro $10/m |
| **GitHub Projects** | ⭐⭐ | 1-20 人 | 跟 code 黏緊 | UI 沒那麼順 | 免費 |

---

### 給學員的決策樹

```
你們是？
├ 第一次跑專案、想簡單一點
│   → Trello
│
├ 喜歡寫文件、會議紀錄想跟 task 整合
│   → Notion
│
├ 99% 時間都在 GitHub 操作 code
│   → GitHub Projects
│
└ 想體驗業界感、不怕學新工具 or 公司 / 學校已經在用 Jira
   → Jira

```

**個人推薦**：**Notion or Trello**。

理由：你已經在用 GitHub 寫 code、開 PR、開 Issue —— 多開一個工具就多一個「記得去更新」的負擔。GitHub Projects 直接跟 Issue / PR 雙向綁定，task 狀態自動更新。

---

### [補充]GitHub Projects 快速設定

1. 進你的 repo → Projects → New project
2. 選 **Table** view + **Board** view 兩個
3. 在 Settings → Custom fields 加：
   - `Sprint` (single select：Sprint 1 / 2 / 3 / Backlog)
   - `Priority` (single select：P0 / P1 / P2 / P3)
   - `Owner` (single select：你們組成員)
   - `Estimate` (single select：S / M / L)
4. 建 4 個 view：
   - **Sprint Current**：filter by Sprint=當週
   - **Backlog**：filter by Sprint=Backlog
   - **My Tasks**：filter by Owner=me
   - **By Module**：group by Label
5. 把所有 Issue 都拉進這個 Project

每個 sprint planning 用 board view 拖拉，把 Backlog 的 issue 拉到當週 sprint。

---

### Trello 簡易設定（如果走輕量路線）

開 5 個 list：

```
📥 Backlog       還沒排程的
🎯 This Sprint   本週要做
🚧 In Progress   進行中（限 3 張，超過要先做完才能新開）
👀 Review        等 review
✅ Done           本週完成
```

每張卡至少有：
- title（動詞開頭）
- description（acceptance criteria）
- assignee（一人）
- due date
- labels（模組 / 優先級）

WIP 限制（In Progress 限 3 張）超過就要先 finish 一張才能開新的 —— 這是 Kanban 精髓。

---

### 不管哪個工具，這 5 件事不能省

1. **每個 task 有明確 owner**(可以一起做 但要有一個主負責人)
2. **每個 task 有簡單的完成條件(例如：資料能成功抓下、DB在雲端環境能成功建立)**
3. **狀態流轉清楚**：Backlog → Sprint → In Progress → Review → Done
5. **每週要確認有哪些在 In Progress**：超過一週的 task = 暗藏問題
6. **試著跟 Git commit 連動**：commit / PR 提到 issue 編號（#123）自動關聯

---

## Part 4：自動化整合（ nice-to-have）

如果還有時間，加這些讓專案看起來更專業：

### 1. GitHub → Discord 通知

```yaml
# .github/workflows/notify.yml
- 新 PR / Issue 自動發到 #review channel
- CI 失敗發到 #alerts
```

### 2. Standup 自動提醒 Bot

Discord Bot（如 Donut / Standup Bot）每天 09:30 推：
> @everyone 該貼 standup 啦：昨天 / 今天 / 卡

### 3. Sentry → Discord

pipeline 失敗自動通知到 #alerts，不靠人手動看

### 4. GitHub Actions 跑 weekly report

每週日自動把：
- 本週 merged PRs
- 本週 closed issues
- 各 owner commits 數
- 沒動的 issues（超過 7 天）

整理成 markdown 留在 `docs/weekly-reports/`

---

## 🎯 小作業：把協作基建一次架好

前置期結束前完成，不然 Sprint 1 開始會混亂。做完 = 你們的協作基建跟業界小團隊一致。

- [ ] **選工具組合**（推薦：Discord + GitHub Projects + GitHub Issues）
- [ ] **開好溝通工具 channels**（依本章 channel 設計，至少 #announce / #standup / #help / 模組 channels）
- [ ] **PM 工具設好**（GitHub Projects + 4 個 views，或 Trello / Notion 5 個 list）
- [ ] **把 Sprint 1 任務都建成 Issue / card** + assign owner + acceptance criteria
- [ ] **約定異步 daily check-in 時間**（建議每天 09:30）+ 形式
- [ ] **約定 Sprint Planning / Sprint Review 兩個會議的固定時段**（每週各一次，60 分鐘）
- [ ] **設 1-2 個自動化通知**（GitHub PR / Sentry → Discord/Slack）

**交付**：把工具清單 + 會議時段表 + 第一張任務看板的截圖貼到指定 channel。

> 💡 工具沒選好 = 接下來整個學期都在切換 + 找訊息。前置期多花 1-2 小時，後面每個 sprint 都會更順。

---

← [回到 README](README.md) | 下一步：[03 小組專案 10 階段流程把這些觀念套用進去 →](03-team-process.md)
