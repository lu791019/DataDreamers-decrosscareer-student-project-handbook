# tests/

> 80% coverage 是業界最低門檻、面試會問。

## 結構

```
tests/
├── unit/            # 單元測試（不依賴外部）
│   ├── ingest/
│   ├── analytics/
│   └── serve/
├── integration/     # 整合測試（用 docker compose 起）
│   └── test_e2e.py
└── conftest.py      # 共用 fixtures
```

## 怎麼跑

```bash
pytest                          # 全部
pytest tests/unit              # 只跑 unit
pytest -k "classifier"         # 只跑名稱含 classifier
pytest --cov=src --cov-report=html  # 含覆蓋率
```

## 寫測試的原則

1. **AAA**：Arrange / Act / Assert 三段清楚
2. **獨立**：測試之間不能依賴順序
3. **fixtures 處理 setup**：用 `conftest.py`
4. **mock 外部依賴**：API / DB / time
5. **每個 bug fix 都要附對應測試** — 不能再犯

## 範例

```python
# tests/unit/analytics/test_classifier.py
def test_classifier_returns_valid_category(mock_openai):
    # Arrange
    classifier = Classifier(api_key="fake")
    article = {"title": "Service down", "content": "..."}

    # Act
    result = classifier.classify(article)

    # Assert
    assert result.category in ["FEE", "CARD", "SYSTEM", "OTHER"]
    assert 0 <= result.confidence <= 1
```

## CI 跑什麼

每個 PR：
- `pytest` 全綠
- coverage 不下降
- ruff + black 通過

詳見 `.github/workflows/ci.yml`
