# {Project Name}

> 一句話描述：為 {who} 解決 {what} 問題。

[Live Demo](https://your-streamlit.app) · [Architecture](docs/architecture.md) · [Demo Video](https://youtube.com)

![demo gif](docs/demo.gif)

---

## 為什麼做這個

{2-3 段：業務痛點 + 量化現況 + 目標差距}

---

## 系統架構

[完整架構圖](docs/architecture.md)

```
Source → Ingest → Storage → Process → Serve → Observe
```

## 快速開始

### Prerequisites
- Docker Desktop
- Python 3.11+
- {可能的 API key}

### 5 分鐘跑起來
```bash
git clone https://github.com/yourteam/{project}.git
cd {project}
cp .env.example .env  # 填入你的 API keys
docker compose up -d
```

訪問：
- Dashboard: http://localhost:8501
- Airflow: http://localhost:8080
- API docs: http://localhost:8000/docs

---

## 技術棧

| 階段 | 工具 |
|---|---|
| Source | {例：Spotify API, Kaggle CSV} |
| Ingest | Python + Airflow |
| Storage | MongoDB / MySQL |
| Process | pandas / SQL / dbt |
| Serve | Streamlit / FastAPI |
| Observe | Sentry / LINE Notify |

---

## 文件

- [PLAN.md](PLAN.md) — 設計與實作計畫
- [task.md](task.md) — 進度追蹤
- [GUIDE.md](GUIDE.md) — 專案導覽
- [docs/architecture.md](docs/architecture.md) — 架構詳解
- [docs/api-contract.md](docs/api-contract.md) — 模組間 API
- [docs/data-dictionary.md](docs/data-dictionary.md) — 欄位定義
- [docs/retro/](docs/retro/) — Sprint 復盤紀錄

---

## 團隊

| 成員 | 角色 | GitHub |
|---|---|---|
| {Name} | Ingest Owner | @user1 |
| {Name} | Pipeline Owner | @user2 |
| {Name} | Analytics Owner | @user3 |
| {Name} | Product Owner | @user4 |

---

## License

MIT
