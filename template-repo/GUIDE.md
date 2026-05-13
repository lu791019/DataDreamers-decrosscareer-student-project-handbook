# 專案導覽（GUIDE）

> 給「第一次來」的人 5 分鐘了解這個 repo。

---

## 這個 repo 是什麼

{一段：解什麼問題、給誰用、目前到哪個階段}

---

## Repo 結構

```
{project}/
├── src/
│   ├── ingest/       # 資料進料模組
│   ├── pipeline/     # 排程與轉換
│   ├── analytics/    # 分析與模型
│   └── serve/        # API / dashboard
├── tests/            # 單元 + 整合測試
├── docs/             # 文件
├── data/             # gitignore，本地放資料
├── notebooks/        # 探索用
├── dags/             # Airflow DAG
└── docker-compose.yml
```

---

## 開發約定

### 跑起來
```bash
cp .env.example .env  # 填 secret
docker compose up -d
```

### 跑測試
```bash
pytest                 # 全部
pytest tests/unit      # 只跑 unit
pytest -k "ingest"     # 只跑 ingest 相關
```

### Lint
```bash
ruff check .
black --check .
```

### 開新 feature
```bash
git checkout develop
git pull
git checkout -b feature/dex-spotify-ingest
# ...開發 + commit...
git push -u origin feature/dex-spotify-ingest
# 上 GitHub 開 PR
```

### Commit message 範例
```
feat: add Spotify OAuth flow + token refresh

實作 src/ingest/spotify_oauth.py。
含 refresh token 邏輯（過期前 5 分鐘自動 refresh）。

Closes #12
```

---

## 模組依賴

```
ingest → storage (write)
storage → transform (read + write)
transform → serve (read)
全部 → observe
```

各模組 API 契約見 [docs/api-contract.md](docs/api-contract.md)

---

## 環境變數

完整見 `.env.example`。最常用的：

| 變數 | 用途 | 例 |
|---|---|---|
| `OPENAI_API_KEY` | LLM | `sk-...` |
| `MONGODB_URL` | DB | `mongodb://localhost:27017` |
| `AIRFLOW_UID` | Airflow | `50000` |

---

## 常見問題

### Q: docker compose up 起不來
A: 檢查 .env 是否填好；MongoDB / MySQL port 是否被佔用

### Q: pytest 失敗在 conftest
A: 先 `pip install -e .` 把 src 變 package

### Q: Airflow UI 看不到 DAG
A: 檢查 `dags/` 目錄有沒有 mount 進 container；看 Airflow scheduler log

---

## Contributors

| Owner | 模組 |
|---|---|
| @user1 | src/ingest/ |
| @user2 | src/pipeline/ + dags/ |
| @user3 | src/analytics/ |
| @user4 | src/serve/ |

Code review：跨模組者主導，模組 owner 必須 review。

---

## 階段對應

目前完成：Sprint {X}
詳見 [task.md](task.md)
