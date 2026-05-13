## 這個 PR 做什麼

<!-- 一句話描述 -->

## 為什麼

<!-- 為什麼要改 / 解了什麼問題 / 對應哪個 issue -->

Closes #

## 怎麼測試

- [ ] 我跑過 `pytest` 都過
- [ ] 我手動測過 X 情境
- [ ] 我加了新測試覆蓋新邏輯

## 截圖 / Log

<!-- 如果改了 UI：放截圖
     如果改了 CLI：貼輸出
     如果是 pipeline：貼 Airflow / Sentry 連結 -->

## 影響範圍

- [ ] 改了 DB schema → 需要跑 migration
- [ ] 改了 API contract → 需要通知 frontend / 其他模組
- [ ] 改了 .env → 通知所有人重新 cp
- [ ] 只改文件
- [ ] 只改測試

## Reviewer Checklist

- [ ] commit message 符合 Conventional Commits
- [ ] 沒有 hardcoded secret / API key
- [ ] 有對應的測試
- [ ] 沒有違反專案的 coding style（black + ruff 過）
- [ ] CI 全綠

## 給 Reviewer 的提示

<!-- 任何想讓 reviewer 注意的地方
     例：「請特別看 src/analytics/recommender.py 的演算法選擇」 -->
