# notebooks/

> 探索 / EDA 用。不入 prod、不會被 CI 跑。

## 規則

1. **命名**：`YYYY-MM-DD_{owner}_{topic}.ipynb`
   例：`2026-04-12_dex_audio_feature_exploration.ipynb`

2. **不要在 notebook 寫 prod 邏輯** → 抽到 `src/`
   notebook 只用來：
   - 探索資料
   - 試 prompt
   - 畫圖驗證假設
   - 看 model 效果

3. **commit 前 clear outputs**：
   ```bash
   jupyter nbconvert --clear-output --inplace notebooks/*.ipynb
   ```

4. **大圖 / 大檔案分開放** `data/external/` 或 cloud storage

## 範例 workflow

```
1. 在 notebook 探索（隨意寫）
2. 確定 logic → 抄到 src/ 模組 + 加測試
3. 在 notebook 改成「呼叫 src/」+ 視覺化結果
4. PR 連同 notebook 一起 commit（讓 reviewer 看推理過程）
```

## 共用

- 探索 / 重要發現 → 同步到 `docs/findings.md`
- 給整組看的視覺化 → 截圖到 PR / Discord
