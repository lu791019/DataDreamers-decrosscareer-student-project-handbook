# 03 業界協作 SOP

> 把「會用 git push」升級成「會跟其他工程師協作」的具體規範。所有 artifact 都有現成樣板可以直接套用。

---

## 為什麼這篇很重要？

> **協作能力比技術深淺更難在履歷上看見，但在面試裡卻會被一眼看穿。**

面試官開你 GitHub 看作品集，第二件事通常是（第一件是 README）：
- 開 commits 看 — 是不是大多只有「update」「fix」？
- 開 PR 看 — 有沒有 review？討論深度？
- 開 Issue 看 — 有沒有 issue tracking？

這些都不是「比技術」，是「比有沒有跟別人協作過」。
這篇給你全套樣板，照抄就有，省下你「不知道從哪開始」的時間。

---

## 1. Repo 結構（fork [template-repo/](template-repo/) 直接用）

```
project-name/
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md
│   │   ├── feature_request.md
│   │   └── question.md
│   ├── PULL_REQUEST_TEMPLATE.md
│   └── workflows/
│       └── ci.yml                 # GitHub Actions 自動測試
├── docs/
│   ├── architecture.md            # 系統架構圖（必要）
│   ├── api-contract.md            # 模組間 API
│   ├── data-dictionary.md         # 欄位定義
│   ├── retro-template.md          # Sprint 復盤模板
│   └── demo-script.md             # Demo 講稿
├── src/
│   ├── ingest/                    # 進料模組
│   ├── pipeline/                  # 排程 / 轉換
│   ├── analytics/                 # 分析 / 模型
│   └── serve/                     # API / dashboard
├── tests/
│   ├── unit/
│   └── integration/
├── data/
│   ├── raw/         (.gitignore)
│   ├── processed/   (.gitignore)
│   └── README.md    # 說明 data 從哪來、怎麼下載
├── notebooks/                     # 探索用，不入 prod
├── docker-compose.yml
├── Dockerfile
├── requirements.txt / pyproject.toml
├── .env.example                   # 環境變數樣板
├── .gitignore
├── README.md                      # 入口
├── PLAN.md                        # 設計 + 實作計畫
├── task.md                        # 進度追蹤
└── GUIDE.md                       # 專案導覽
```

### 為什麼這樣分？
- `src/` 4 個資料夾＝小組 4 種角色各擁有一個目錄
- `docs/` 寫文件不是裝飾，是必要 artifact
- `data/` 用 `.gitignore` 排除實際資料、只留 README 說明怎麼取得

---

## 2. Branch 命名規範

```
main            ← 永遠可部署 ⚠️ 任何人不准直接 push
└── develop     ← 開發主幹，所有 feature 合進來
    ├── feature/{owner}-{topic}    例：feature/dex-airflow-setup
    ├── fix/{owner}-{topic}        例：fix/amy-empty-row
    ├── docs/{owner}-{topic}       例：docs/peter-architecture
    └── refactor/{owner}-{topic}
```

### 規矩
1. **main 開 branch protection**：必須 PR + 至少 1 個 approve 才能合
2. **每個 PR 一個小目標**：不要混 feature + fix + refactor
3. **PR 一週內合掉**：超過一週的 branch 變地雷
4. **不准 force push 共用 branch**

---

## 3. Commit Message 樣板

### 格式（Conventional Commits）
```
<type>: <description>

[optional body]

[optional footer]
```

### Type
| Type | 何時用 |
|---|---|
| `feat` | 新功能 |
| `fix` | 修 bug |
| `docs` | 改文件 |
| `refactor` | 重構（不改行為）|
| `test` | 加 / 改測試 |
| `chore` | 雜事（升級套件 / config）|
| `perf` | 效能改善 |
| `ci` | CI 設定 |

### 範例

❌ **爛**：
```
update
fix
WIP
xxx
```

✅ **好**：
```
feat: 加入 Spotify API 拉取每日新歌資料

實作 src/ingest/spotify_client.py，每日抓取 top 50。
加上 rate limit 處理（5 sec retry）。

Closes #12
```

```
fix: 處理 momo 商品頁回傳 404 時的 retry 邏輯

issue #28 中發現商品下架會被當成爬蟲被擋。
改成 404 直接 skip 並 log，其他 5xx 才 retry。
```

```
docs: 補上 dashboard 部署到 Streamlit Cloud 的步驟
```

---

## 4. PR Template（[完整版見 template-repo/.github/PULL_REQUEST_TEMPLATE.md](template-repo/.github/PULL_REQUEST_TEMPLATE.md)）

```markdown
## 這個 PR 做什麼

<!-- 一句話 -->

## 為什麼

<!-- 為什麼要改 / 解了什麼問題 -->

## 怎麼測試

- [ ] 我跑過 `pytest` 都過
- [ ] 我手動測過 X 情境
- [ ] 我加了新測試

## 截圖 / Log

<!-- dashboard 改動截圖、CLI 輸出、log 等 -->

## 影響範圍

- [ ] 改了 schema → 需要跑 migration
- [ ] 改了 API → 需要通知 frontend
- [ ] 只改文件
- [ ] 改了 .env → 通知所有人

## Reviewer checklist

- [ ] commit message 符合規範
- [ ] 有對應的測試
- [ ] 不違反 04 的 code review 守則
- [ ] CI 過了

Closes #
```

---

## 5. Issue Template

3 種：bug / feature / question。內容見 [template-repo/.github/ISSUE_TEMPLATE/](template-repo/.github/ISSUE_TEMPLATE/)。

關鍵原則：**Issue 不是聊天**，是「未來自己 / 別人翻得到的決策紀錄」。每個討論都該變 issue。

---

## 6. Code Review 守則（給 reviewer）

### 看順序
1. **commit message** 是否清楚？看不懂就要求重寫
2. **PR description** 是否回答了「為什麼」？
3. **Code logic** — 有沒有正確性問題？
4. **Code quality** — 命名 / 拆分 / DRY
5. **Tests** — 有沒有測試覆蓋

### Review 留言三種 prefix
```
[blocker] 必須改才能合
[suggest] 建議改、但你決定
[nit]     龜毛、可改可不改、不擋合 PR
```

範例：
```
[blocker] 這裡會 None pointer，傳進來可能是 dict 也可能是 None
[suggest] 這個變數名 data 太籠統，改 spotify_tracks 會更清楚
[nit] 多了一個空行
```

### 不該做的事
- ❌ 「這個寫法不好」← 不告訴對方怎麼改＝沒幫到他
- ❌ 在 PR 留言開戰 ← 改成語音 call
- ❌ 自己 approve 自己的 PR

---

## 7. 溝通節奏

```
每天   daily standup（10 分鐘，文字或語音）
       ├ 昨天做什麼
       ├ 今天要做什麼
       └ 卡什麼 / 需要誰幫

每週一  sprint planning（1 小時）
       └ 認領下週任務

每週五  sprint review（1 小時）
       └ 內部 demo 進度

每週日  sprint retro（30 分鐘）
       ├ 什麼 ok 繼續做
       ├ 什麼不行要停
       └ 下週試什麼
```

### Daily standup 在 Discord / Slack 的訊息樣板
```
昨天：完成 spotify ingest 模組、跑通排程
今天：寫 unit test、開始整合 storage
卡：MongoDB connection timeout（issue #34）→ Peter 幫看
```

> 一定要寫「卡什麼」 — 沒卡的人通常其實有卡。

---

## 8. CI/CD 最低門檻

[`template-repo/.github/workflows/ci.yml`](template-repo/.github/workflows/ci.yml) 已經寫好，包含：

```yaml
- pytest 跑單元測試
- ruff / black 檢查 code style
- mypy 檢查 type（optional）
- 跑得起 docker compose（檢查整合）
```

**最低標準**：每個 PR 都要 CI 過。不過不准合。

---

## 9. 文件三件套（不是裝飾）

| 文件 | 給誰看 | 何時寫 |
|---|---|---|
| `README.md` | 第一次來的人 | W0 就寫 |
| `PLAN.md` | 執行者（你們自己）| W2 設計完寫 |
| `task.md` | 任何人快速看進度 | W3 開工就寫 |
| `GUIDE.md` | 接手者 / 教練 | 半途和最後更新 |

### README 必有元素
```markdown
# 專案名稱

> 一句話描述：為誰解決什麼問題

[螢幕截圖 / GIF]

## 為什麼做這個
## 系統架構（一張圖）
## 快速開始
```bash
make dev    # 5 分鐘內能跑起來
```
## 技術棧
## 團隊
## License
```

### task.md 範本
```markdown
# Tasks

## Sprint 1（W3）
- [x] Spotify ingest（@dex）#12 ed4f3a2
- [x] MongoDB schema（@peter）#15 a8b912c
- [ ] Streamlit MVP（@amy）#18

## Sprint 2（W4）
- [ ] Airflow 排程（@dex）
...
```

---

## 10. 一個業界級小組的「一天」長這樣

```
09:30  打開 Discord 看 #standup
       讀別人的進度、自己貼 standup

09:45  打開 GitHub
       看有沒有 PR 等我 review
       看分配給我的 issue

10:00  開 IDE，pull develop，開 feature branch
       開始今天的任務

12:00  push 一版 → 開 PR → assign reviewer

14:00  reviewer 留言 → 改 → 再 push

15:00  PR approve → squash merge → 關 issue

15:30  寫今天的成果到 task.md
       明天 standup 講什麼想好

週五   sprint review demo 10 分鐘
週日   retro 30 分鐘 → 寫進 docs/retro/week-N.md
```

---

下一步：[04 8 情境痛點 × 業界對應地圖 →](04-pain-points-industry-map.md)
