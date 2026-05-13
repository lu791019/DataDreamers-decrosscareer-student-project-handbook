# Sprint Retro 模板

> 每個 Sprint 結束週日花 30 分鐘做。寫成檔案放 `docs/retro/sprint-{N}.md`。

---

## 範例：Sprint 1 Retro

```markdown
# Sprint 1 Retro - 2026-04-05

**Sprint 目標**：端到端跑通最小 pipeline

**完成度**：80%（4 task / 5）

**參與者**：@dex @amy @peter @sue

---

## Keep（繼續做）

- 每天 standup 10 分鐘，所有人都有貼進度
- 用 PR template 後 review 速度變快（從平均 1 天 → 4 小時）
- Amy 把 docker-compose 一次寫好，省了大家很多時間

## Problem（要解決）

- ⚠️ T-004 dashboard 沒做完 — 卡在 streamlit OAuth 設定
- ⚠️ 兩次 schema 改動沒先告知，造成 Peter 整天 work 卡掉
- ⚠️ Sentry 一直在響但沒人看 → 學到「監控也要有人 onCall」

## Try（下週試試）

- [ ] 開個 Discord channel #alerts 把 Sentry 倒進去
- [ ] Schema 改動先開 issue 標 [schema-change]，至少等 1 個 approve
- [ ] OAuth 部分配對寫，Sue 跟 Amy 一起 pair

## Action items（下週前完成）

- [ ] @amy 加 Sentry → Discord webhook（issue #41）
- [ ] @peter 補一份 schema 變更 PR template
- [ ] @sue + @amy 週一 9-12am pair OAuth

---

## 數據

- Commits this sprint: 67
- PRs merged: 14
- PRs open at sprint end: 3
- Issues created: 22
- Issues closed: 17
- 開會時數: 6 hr / 人
- Coding 時數: 12 hr / 人
```

---

## KPT 簡化版（10 分鐘版本）

如果時間緊，最少寫這三條：

```markdown
# Sprint N Retro - YYYY-MM-DD

## Keep
-

## Problem
-

## Try
-
```

---

## 4Ls 模板（適合 final retro）

```markdown
# Final Retro - 2026-05-30

## Liked（喜歡的）
-

## Learned（學到的）
-

## Lacked（不足的）
-

## Longed for（希望有的）
-
```

---

## Sailboat 模板（適合需要視覺化）

畫成圖會更生動，但文字版也行：

```markdown
🏝 **目標**：穩定的每日資料更新

⬆️ **風（推進力量）**：
- Airflow 自動排程
- 組員技能互補

⚓ **錨（拖累力量）**：
- 沒人做 documentation
- Code review 卡 2 天

🦈 **鯊魚（風險）**：
- 雲端額度快用完
- 期末週兩個人有別的考試

🪨 **暗礁（過去的坑）**：
- 第 3 週浪費 2 天設定 docker
```

---

## Retro 守則

1. **對事不對人**：說「PR review 慢」不說「Peter 都不 review」
2. **可行動**：每條 Try 都要寫成 action items + assignee
3. **誠實**：寫「都很好」的 retro = 沒做 retro
4. **下個 sprint 開始前回顧**：sprint planning 第一件事看上次 retro 的 action items

---

## 個人 retro（Final 時做）

每個人先自己寫，再合併：

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

## 4. 下次想加強的技能（具體、可量化）
- [ ] 在 X 時間前學會 Y

## 5. 給組員的 feedback（每人 1 條）
- @組員A：你的 X 很強 / 你可以加強 Y
- ...

## 6. 給 3 個月後自己的話
（一封信，會在 demo 完後寄出）
```
