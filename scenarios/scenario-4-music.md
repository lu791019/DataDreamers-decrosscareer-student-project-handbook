# 情境 4：音樂串流推薦優化 + 用戶偏好

> **一句話**：給音樂愛好者「跟你最近聽的歌氛圍類似但你還沒聽過」的推薦清單。

---

## 為誰解什麼

- **目標用戶**：每天聽歌 30+ 分鐘、覺得 Spotify 推薦同質化的人
- **痛點**：歌單越來越窄、新歌很少被推、想嘗鮮但不知道從哪找
- **量化目標**：推薦清單中「用戶會 add to playlist」的比例 ≥ 20%

---

## 業界對標

→ 詳見 [04 痛點地圖 - 情境 4](../04-pain-points-industry-map.md#情境-4音樂串流推薦優化--用戶偏好)

**過往學長姐 demo**：
- [03 KKBOX & Spotify 音樂串流市場比較分析（TIR102）](https://youtu.be/esk9n-bXJCY)
- [01 SteamTrend（TIR102）](https://youtu.be/Sbrw5Z2UOiE)

---

## 6 階段藍圖具體化

```
Source              Ingest              Storage         Process             Serve           Observe
─────               ──────              ───────         ─────────           ─────           ───────
Spotify Web API    requests + retry    MongoDB         pandas + SQL          Streamlit       Airflow UI
Spotify Charts     Airflow 每日        (tracks /        + sklearn            + Spotify       + cost watcher
Kaggle KKBOX       (rate limit 30/sec) listenings /     (audio features      OAuth login     + API rate
                                       playlists)        + 分群 + 推薦）                       monitoring
```

---

## 資料源細節

| 資料源 | 取得方式 | 規模 | 用來做 |
|---|---|---|---|
| [Spotify Web API](https://developer.spotify.com/documentation/web-api) | OAuth + REST | 自己歌單 + audio features | 個人推薦 |
| [Spotify Charts](https://charts.spotify.com/) | 公開 CSV | Top 200 / 國家 / 日 | 趨勢分析 |
| [Kaggle KKBOX Music Recommendation](https://www.kaggle.com/c/kkbox-music-recommendation-challenge) | 下載 | 數百萬筆聽歌紀錄 | 大規模訓練 |

---

## 10 階段執行重點

### ① 啟動
- 選題理由：音樂是「人人都用得到」的 demo，技術涵蓋面廣
- 強烈建議：選一個你「真的天天用」的串流平台

### ② Discovery
- Persona 範例：阿凱 26 歲、通勤聽歌、抱怨推薦同質化
- 痛點：(1) 推薦來來去去都那幾首 (2) 想嘗鮮但 mood-based 找不到 (3) 沒法跟朋友比對品味

### ③ 設計
- 推薦演算法：
  - v1: collaborative filtering（協同過濾）
  - v2: audio features clustering（cluster 後推同 cluster 的）
  - v3: embedding-based（用 song name + artist text embedding）
- Schema：tracks / listening_history / audio_features / recommendations

### ④ 分工
| 角色 | 任務 |
|---|---|
| Ingest | Spotify API + OAuth flow + rate limit |
| Pipeline | Airflow daily refresh + MongoDB |
| Analytics | 推薦演算法 v1 → v3 + 評估 |
| Product | Streamlit + Spotify login + 推薦清單 |

### ⑤ 環境
- Spotify Dev account 註冊
- OAuth redirect URI 設定要早 — 部署前常忘

### ⑥ 衝刺

**Sprint 1（W10-W12）**：
- 用自己帳號跑通 OAuth + 抓 50 首歌
- MongoDB 存
- 跑 v1 推薦

**Sprint 2（W13-W15）**：
- 整套 pipeline 自動跑
- v2 + v3 推薦演算法
- Streamlit 雛形

**Sprint 3（W16-W18）**：
- 推薦評估（給用戶看、收 feedback）
- 多用戶（組員 3 人）測試
- UI 優化

### ⑦ 整合
- 端到端：登入 → 抓最近聽的歌 → 算推薦 → 顯示
- 整合測試：組員 4 個帳號都跑通

### ⑧ 上線
- Streamlit Cloud（OAuth callback 注意設定）
- Airflow 跑在 GCP

### ⑨ Demo
強調「**用戶會買單的價值**」：
1. 真的給聽眾測試（用 organizer 帳號）
2. 講 conversion：「測試 5 人有 4 人 add to playlist」
3. 對比 Spotify 內建推薦的差異

### ⑩ 復盤

---

## 範例：audio features 推薦邏輯

```python
# Spotify audio features 13 維（danceability, energy, valence, ...）
# 對一首歌算「氛圍向量」

def recommend(user_id: str, top_k: int = 20):
    # 1. 拿用戶最近聽的 50 首歌
    recent = get_recent_tracks(user_id, n=50)

    # 2. 算「氛圍中心」(centroid)
    centroid = audio_features(recent).mean(axis=0)

    # 3. 從全庫找氛圍向量最近、且用戶沒聽過的歌
    candidates = (
        track_pool
        .filter(~Track.id.in_(user_history(user_id)))
        .compute_distance_to(centroid)
        .sort_by("distance")
        .limit(top_k)
    )
    return candidates
```

---

## 範例 commit log

```
* feat: Spotify OAuth flow + token refresh (#3)
* feat: ingest recent tracks API endpoint (#5)
* feat: MongoDB schema for tracks/listenings/features (#7)
* feat: collaborative filtering recommendation v1 (#10)
* feat: audio features clustering v2 (#14)
* feat: embedding-based recommendation v3 (#18)
* test: A/B compare 3 algorithms on 5 user sessions (#21)
* feat: Streamlit dashboard with Spotify login (#24)
* docs: ADR-002 - why v3 over v1/v2 (#26)
```

---

## 進階挑戰

- [ ] **Vector DB（pgvector / Pinecone）**：把歌曲 embedding 存 vector DB，毫秒級近鄰查詢
- [ ] **多模態**：加 album cover 圖像 embedding
- [ ] **時段感知**：通勤推 chill / 健身推 energy
- [ ] **跨平台**：同時整合 KKBOX 抓 KKBOX 用戶歌單

---

## 雷區

| 雷 | 為什麼 |
|---|---|
| 沒做 OAuth refresh | token 1 小時過期 demo 翻車 |
| 推「最熱門」 | 那叫排行榜不叫推薦 |
| Audio features 沒 normalize | clustering 結果偏 |
| Demo 用同一個帳號 | 看不出個人化價值 |

---

## 完整時程（總 20 週）

| 週 | 階段 | 重點產出 |
|---|---|---|
| W1-W3 | 啟動 | Spotify Dev account |
| W2-W4 | Discovery | 推薦演算法選型 |
| W4-W7 | 設計 + 分工 | OAuth + schema |
| W10-W12 | Sprint 1 | OAuth + 50 首 + v1 推薦 |
| W13-W15 | Sprint 2 | 自動化 + v2/v3 + dashboard |
| W16-W18 | Sprint 3 | 多用戶測試 + 評估 |
| W19 | 整合 + 上線 | Streamlit Cloud + OAuth deploy |
| W20 | Demo + 復盤 | conversion 數據 |

---

← [上個情境：3 數位金融](scenario-3-fintech.md) | 下個情境：[5 叫車交通 →](scenario-5-ride.md)
