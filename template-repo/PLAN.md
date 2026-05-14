# 實作計畫

> 給執行者看的食譜：什麼要做、怎麼做、做完長什麼樣。

---

## 1. 問題定義

### 目標用戶 Persona
{至少 1 個具體 persona — 寫到能「看到這個人」的程度}

### 核心痛點
1. {可量化痛點 1}
2. {可量化痛點 2}
3. {可量化痛點 3}

### 成功標準
- [ ] 指標 1：{X 從 Y 變 Z}
- [ ] 指標 2：{...}

---

## 2. 系統設計

### 6 階段對應
| 階段 | 工具 | 為什麼選這個 |
|---|---|---|
| Source | | |
| Ingest | | |
| Storage | | |
| Transform | | |
| Serve | | |
| Observe | | |

### 資料模型
參見 [docs/data-dictionary.md](docs/data-dictionary.md)

### API 契約
參見 [docs/api-contract.md](docs/api-contract.md)

---

## 3. Sprint 計畫

### Sprint 1（W10-W12）— 端到端跑通
**目標**：1 條完整 pipeline 跑得起來，醜沒關係

**任務**：
- [ ] T-001 {ingest 第一個資料源}
- [ ] T-002 {storage schema 建立}
- [ ] T-003 {一個基本 transform}
- [ ] T-004 {一個簡單 dashboard 顯示結果}

**完成標準**：能從 source 跑到 dashboard 看到資料

---

### Sprint 2（W13-W15）— 擴充 + 自動化
**目標**：加排程 + 擴資料 + 加分析深度

**任務**：
- [ ] T-101 ...
- [ ] T-102 ...

---

### Sprint 3（W16-W18）— 打磨 + 監控
**目標**：可以給別人用、出問題你會知道

**任務**：
- [ ] T-201 ...

---

## 4. 風險清單

| 風險 | 影響 | 緩解 |
|---|---|---|
| {API rate limit} | 中 | {batch 處理 / 多 key 輪詢} |
| {組員某週缺席} | 高 | {RACI 副擔接手} |
| {Cloud 額度爆} | 中 | {weekly cost check} |

---

## 5. 不做的事（避免 scope creep）

明確列出「這個 sprint 不做」的：
- 不做 X
- 不做 Y
- 進階功能 Z 推到「課後加強」

---

## 6. 決策紀錄（ADR）

把關鍵設計決定寫成 ADR（Architecture Decision Record）：

### ADR-001：為什麼選 MongoDB 不選 MySQL
- Context
- Decision
- Consequences

### ADR-002：...
