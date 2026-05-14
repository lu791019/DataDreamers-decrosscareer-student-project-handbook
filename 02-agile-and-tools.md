# 02 敏捷開發 + 溝通與專案管理工具選型

> 流程跑得順、訊息傳得清楚、卡關有人接 —— 這三件事決定整個學期能不能順利走完。
> 這篇幫你把「該怎麼跑」和「該用什麼工具」一次想清楚。

---

## Part 1：敏捷開發 — 小組專案的最佳節奏

### 為什麼是敏捷？

學員專案時間有限、組員幾個、需求會變、不會做完美 —— 這正是敏捷被設計來解決的場景。

> 敏捷不是「速度快」，是「願意接受『我們一開始想的不完全對』，然後快速調整」。

直接照搬企業 Scrum 太重；土法煉鋼又會吵架。下面是給「小組專題」剪裁過的版本。

---

### 兩個學派，挑一個用就好

| 學派 | 適合 | 一句話特色 |
|---|---|---|
| **Scrum** | 任務切得出明確邊界、有共同節奏 | 用 sprint 把時間切成等長的格子 |
| **Kanban** | 任務大小差異很大、用戶研究多 | 用看板把流程視覺化、限制同時做的事 |

**90% 的學員小組適合 Scrum**。Kanban 適合做的事很雜、沒固定週期的團隊。

下面用 Scrum 講。

---

### Scrum 五件事（不要省）

```
1. Sprint Planning      週一上午 1 小時     決定本週要做什麼
2. Daily Standup        每天 10 分鐘        互相同步、找卡關
3. Sprint Review        週五下午 1 小時     對組內 / 教練 demo
4. Sprint Retrospective 週日 30 分鐘         反省與調整
5. Backlog Refinement   週中 30 分鐘（彈性） 把下週要做的整理清楚
```

> 不開 daily 是學員小組最常見的死法。10 分鐘的代價，換的是「一個人卡 3 天沒人發現」的避免。

---

### Sprint Planning 怎麼開（給第一次跑的人）

**前置**：[03 階段流程](03-team-process.md) 寫好的 PLAN.md。

**會議流程（60 分鐘）**：

```
00-10 min   回顧上週進度（task.md 打勾的、沒打勾的）
10-15 min   讀上週 retro 的 action items
15-40 min   挑下週要做的任務（從 PLAN 的 sprint 清單）
            ── 每個任務有：owner、估時、acceptance criteria
40-55 min   風險討論（誰可能卡住、誰會缺席、API 額度…）
55-60 min   結論 + 把任務寫進 task.md
```

**估時用 T-shirt size 就好**：
- S = 半天可以做完
- M = 1-2 天
- L = 3-4 天（超過 L 就要拆）

不要用「story point」這種雞肋的東西，學員小組沒必要。

---

### Daily Standup — 10 分鐘版本

**時間**：固定每天上午（建議 09:30 或 10:00）

**形式**：
- 同步開會 / 文字接龍 / 異步貼 Discord 都行
- 文字版反而省時間、有紀錄

**每人 3 句**：
```
昨天：我做了 X
今天：我打算做 Y
卡：我卡在 Z，需要 {誰} 幫
```

**如果沒卡，也要明確說「沒卡」** —— 不然不知道是真的順還是不想講。

---

### Sprint Review — 不是 Demo Day 排練

很多學員以為這就是練 demo —— 不是。

**Review 的真正目的**：
- 對「自己人」demo，看「東西是不是真的能用」
- 收 feedback 給下個 sprint 用
- 教練 / 同學在這時候給意見成本最低

**結構（60 分鐘）**：
```
0-15 min   product owner 講「這 sprint 做了什麼」
15-35 min  Live demo（不要投影片）
35-50 min  Q&A + 反饋
50-60 min  決定哪些反饋進下週 backlog
```

---

### Sprint Retro 5 個常用句型

retro 在 [06](06-retro-and-after.md) 已詳述。補充給卡住的人：

| 場合 | 句型 |
|---|---|
| 想講不順但怕傷人 | 「我發現 X 流程讓我們慢下來，不知道大家怎麼看？」 |
| 想稱讚但不肉麻 | 「我覺得 Y 做得很穩，未來想學起來」 |
| 不確定該不該講 | 「不一定要做，但我想分享一個觀察⋯」 |
| 想推動行動 | 「下週要不要試試 Z？如果不行下下週就回原本」 |
| 想結束無解討論 | 「這個我們今天決定不了，先當未解列下次再聊」 |

---

### Velocity（速度感）— 小組怎麼用

別套企業那種「我們 sprint velocity 是 23」這種數字。

**學員小組用感覺就好**：
- Sprint 1 你們完成了 60%
- Sprint 2 提升到 80%
- Sprint 3 拉到 90%

如果一直在 50%，要做的不是「逼自己快一點」，是「砍 scope」。

---

### 砍 scope 的藝術

學員專案最大的死因不是「做不出來」，是「沒有勇氣砍」。

**砍的優先順序**：

```
must have    ← 砍掉 demo 沒得展、絕對不能砍
should have  ← Sprint 2 才考慮砍
nice to have ← 第一個被砍
delight      ← 想做但不要列進 sprint
```

把 PLAN.md 每個 task 標上這 4 級。Sprint 中遇到延遲，從 nice → should 往上砍。

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

#### 推薦 1：Discord + Notion + GitHub（最多人用）

| 工具 | 用途 | 為什麼 |
|---|---|---|
| **Discord** | daily standup / 即時討論 / voice call | 免費 / 多 channel / 整合機器人方便 |
| **Notion** | 會議紀錄 / 文件 / PLAN 中間版 | 共編好、好搜尋 |
| **GitHub Issues** | task / bug / 決策紀錄 | 跟程式碼放一起、追溯方便 |

> 適合：第一次組隊、想學業界協作流程的小組。

#### 推薦 2：LINE + Google Drive + GitHub

| 工具 | 用途 | 為什麼 |
|---|---|---|
| **LINE 群組** | 即時討論 / 提醒 | 大家本來就有、學習曲線零 |
| **Google Docs / Sheets** | 共編文件 | 老一輩 / 業界都會用 |
| **GitHub Issues** | task | 同上 |

> 適合：組員背景差距大（有非工程背景）、不想學新工具。

#### 推薦 3：Slack + Linear + GitHub（業界感最強）

| 工具 | 用途 | 為什麼 |
|---|---|---|
| **Slack** | 同 Discord | 業界主流、未來工作會用到 |
| **Linear** | task / sprint 管理 | 比 Trello 強、快、好看 |
| **GitHub Issues** | 程式碼相關討論 | 跟 Linear 雙向同步 |

> 適合：想直接體驗業界工作流的小組。注意 Linear 個人版 free、Slack 免費版有訊息歷史限制。

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

> Dex 建議：學員專題用 **Discord** —— 學習曲線適中、機器人整合方便、學完還能用在其他社群活動。

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

**threading 規則**：每個討論起一條 thread，主 channel 只放一個總結。不然搜尋會崩。

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
| **Linear** | ⭐⭐⭐ | 5-30 人 | 速度快 / 業界感強 | 個人版功能受限 | 免費 10 user |
| **Jira** | ⭐⭐⭐⭐⭐ | 20+ 人企業 | 企業級權限 | 殺雞用牛刀 | $$ |

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
├ 想體驗業界感、不怕學新工具
│   → Linear
│
└ 公司 / 學校已經在用 Jira
    → Jira（不要切換）
```

**Dex 個人推薦**：**GitHub Projects**。

理由：你已經在用 GitHub 寫 code、開 PR、開 Issue —— 多開一個工具就多一個「記得去更新」的負擔。GitHub Projects 直接跟 Issue / PR 雙向綁定，task 狀態自動更新。

如果組裡有美感控、想要好看的看板：**Linear**（但要花 30 分鐘 onboard）。

---

### GitHub Projects 快速設定（推薦組合）

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

1. **每個 task 有明確 owner**（不准「大家一起」）
2. **每個 task 有 acceptance criteria**（怎樣算完成？）
3. **狀態流轉清楚**：Backlog → Sprint → In Progress → Review → Done
4. **每週清一次 In Progress**：超過一週的 task = 暗藏問題
5. **跟 Git 連動**：commit / PR 提到 issue 編號（#123）自動關聯

---

## Part 4：自動化整合（拉滿一些 nice-to-have）

如果還有時間，加這些讓專案看起來更專業：

### 1. GitHub → Discord/Slack 通知

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

## 總結：第一週要做的 7 件事

```
□ 1. 選工具組合（推薦：Discord + GitHub Projects + GitHub Issues）
□ 2. 開好 Discord channels（依上面結構）
□ 3. GitHub Projects 設好 + 4 個 views
□ 4. 把第一週的 task 都建成 Issue + assign owner
□ 5. 約定 daily standup 時間 + 形式
□ 6. 約定 sprint planning / review / retro 三個固定會議時間
□ 7. 開 1-2 個自動化通知（GitHub → Discord）
```

做完 = 你們的協作基建跟業界小團隊一致。

---

## 🎯 小作業：把協作基建一次架好

W0 結束前要完成，不然 Sprint 1 開始會混亂。

- [ ] 選好溝通工具（Discord / Slack / LINE 三選一）+ 開好 channels（依本章 channel 設計）
- [ ] 選好 PM 工具（GitHub Projects / Trello / Linear 三選一）+ 把 Sprint 1 任務都建成 issue/card
- [ ] 約定 daily standup 形式（同步 / 異步）+ 固定時間
- [ ] 約定 sprint planning / review / retro 三個會議的固定時段
- [ ] 至少設 1 個自動化（GitHub PR → Discord/Slack 通知）

**交付**：把工具清單 + 會議時段表 + 第一張任務看板的截圖貼到指定 channel。

> 💡 工具沒選好 = 接下來整個學期都在切換 + 找訊息。前置期多花 1-2 小時，後面每個 sprint 都會更順。

---

← [回到 README](README.md) | 下一步：[03 小組專案 10 階段流程把這些觀念套用進去 →](03-team-process.md)
