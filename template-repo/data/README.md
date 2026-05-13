# data/

> 實際資料 **不入 git**（已 .gitignore），只有這份說明 + sample。

## 結構

```
data/
├── raw/             # 原始下載（gitignore）
├── processed/       # 清洗後（gitignore）
├── interim/         # 中間產物（gitignore）
├── external/        # 第三方靜態資料（gitignore）
├── sample.csv       # 給跑測試用的小樣本（commit）
└── README.md        # 你正在看的這份
```

## 怎麼取得真實資料

### Source 1：{資料源名稱}

**取得方式**：
```bash
# 範例
python -m src.ingest.{source1} --start 2025-01-01 --end 2026-05-01
```

**輸出位置**：`data/raw/{source1}/YYYY-MM/`
**檔案格式**：parquet
**大小**：~500 MB / 月

### Source 2：{資料源名稱}

**取得方式**：
1. 註冊 https://...
2. 取得 API key 放 `.env`：`SOURCE2_API_KEY=...`
3. 跑：
```bash
python -m src.ingest.{source2} --daily
```

---

## Sample data

`data/sample.csv`：100 筆代表性樣本，給 unit test 用。

不要在 sample 放個資 / 敏感資料！

---

## 不要做的事

- ❌ 不要 `git add data/raw/`
- ❌ 不要把 API response 直接貼上 PR description
- ❌ 不要在 docs 放真實人名 / 帳號
- ❌ 不要 commit > 100 MB 的東西

## 容量管理

定期清理：
```bash
# 保留最近 30 天
find data/raw -mtime +30 -delete

# 清空 interim（隨時可重跑）
rm -rf data/interim/*
```
