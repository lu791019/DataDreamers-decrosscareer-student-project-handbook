# 專案協作第 0 週 ｜ 00 GitHub 註冊、開通與 Fork SOP

> 沒用過 GitHub？這篇給你最快的路徑。不重寫一遍別人寫好的教學 — 我們直接指你去看最棒的。

---

## 為什麼你需要 GitHub 帳號？

| 情境 | 沒 GitHub | 有 GitHub |
|---|---|---|
| 面試 | 只能用講的 | 打開 github 證明 |
| 找專案 | 找不到 | star / fork / 追蹤 trending |
| 跟組員協作 | 用 LINE / Dropbox 傳 code | 用 PR / Issue |

---

## 推薦學習資源

以下挑一份看就夠：

| 資源 | 適合 | 連結 |
|---|---|---|
| 🐢 **30 天精通 Git** | 想紮實學底層概念 | [doggy8088/Learn-Git-in-30-days](https://github.com/doggy8088/Learn-Git-in-30-days/tree/master/zh-tw) |
| 🦀 **Git Tutorials by twtrubiks** | 想看實例 / commit / branch / rebase 範例 | [twtrubiks/Git-Tutorials](https://github.com/twtrubiks/Git-Tutorials) |
| 📚 **Git with GitHub** | 想快速上手 + 知道每個指令在幹嘛 | [hackmd.io/@sysprog/git-with-github](https://hackmd.io/@sysprog/git-with-github) |

額外備案：
- 官方互動式教學：[learngitbranching.js.org](https://learngitbranching.js.org/?locale=zh_TW)（玩遊戲學 branch / merge / rebase）
- Pro Git 中文版（最權威）：[git-scm.com/book/zh-tw/v2](https://git-scm.com/book/zh-tw/v2)

---

## 4 步驟 onboard

### Step 1 — 註冊 + 設定帳號（10 分鐘）

1. https://github.com/signup 註冊
2. 設好 Profile（大頭照、Bio、Location）：https://github.com/settings/profile
3. 開兩階段認證：https://github.com/settings/security
4. 開一個跟 username 同名的 repo + README — 這會變你的 GitHub 名片首頁

### Step 2 — 本機環境

[Github 本機安裝](https://git-scm.com/book/zh-tw/v2/%E9%96%8B%E5%A7%8B-Git-%E5%AE%89%E8%A3%9D%E6%95%99%E5%AD%B8)


```終端機 CLI 輸入

git --version  # 確認 git 有了

git config --global user.name "你的 GitHub username"
git config --global user.email "你註冊 GitHub 用的 email"
git config --global init.defaultBranch main
```

⚠️ email 務必跟 GitHub 一致，不然 commits 會亂掉。

### Step 3 — 驗證 push 能跑

選一種：
- **HTTPS + Personal Access Token**：最簡單，照 GitHub 提示走
- **SSH key**：之後 push 不用打密碼，[官方教學](https://docs.github.com/zh/authentication/connecting-to-github-with-ssh)

驗證：
```終端機 CLI 輸入
# HTTPS 直接 clone 試試
git clone https://github.com/lu791019/tibame-student-project-handbook.git

# 或 SSH
ssh -T git@github.com
```

### Step 4 — 裝 gh CLI（不一定需要）

```終端機 CLI 輸入

# macOS
brew install gh

# Windows
winget install --id GitHub.cli

gh auth login  # 一條指令登入
```

---

## 常見問題

**Q: "Author identity unknown"**
→ 沒設 `git config user.email`，回 Step 2

**Q: "Permission denied (publickey)"**
→ SSH key 沒加進 GitHub，看 Step 3 SSH 連結

**Q: "protected branch"**
→ 不能直推 main，要走 PR：
```bash
git checkout -b feature/my-change
git push -u origin feature/my-change
gh pr create  # 或網頁開 PR
```

**Q: 不小心 commit 了 secret（API key）**
→ 立刻 revoke 那個 key、用 [BFG Repo-Cleaner](https://rtyley.github.io/bfg-repo-cleaner/) 從歷史刪掉、重發新 key。預防：永遠用 `.env.example`、`.env` 加進 `.gitignore`。

---

## Github 設定盤點 Checklist

- [ ] 建立 GitHub 帳號
- [ ] 設定 2FA
- [ ] 本機 git config 設好 user.name / user.email
- [ ] 理解或嘗試過 git pull、commit、push 等基礎功能
- [ ] 看過上面 3 份教學至少 1 份

---

## 🎯 小作業：開好各組的專題 repo

分好組、選好情境後，建立「專題共用程式碼和共同協作區域」，也就是「專題用 Repo」建立好

下面提供 **兩種版本** 選一個用：

| 版本 | 適合 | 重點 |
|---|---|---|
| 🌱 **一般版** | 第一次開團隊 repo、想快上手 | 組長個人帳號開 repo + 加組員進入 |
| 🚀 **專業版** | 想接近業界做法、面試代表作要乾淨 | 建立一個 組織 Github， 開團隊主 repo ， 另外每人自己 fork回來，並開 portfolio repo |

> 💡 **沒選擇障礙就選一般版**。專題結束想升級時再 Transfer 到 org 也來得及，程式碼和設定可以搬遷過去不用重寫

---

### 🌱 一般版：組長個人 repo

由組長一人在自己 GitHub 帳號開 repo，將組員加為 collaborator

#### Step 1 — 開 Public repo

**方法 A：用 gh CLI**
```bash
gh repo create your-team/G3-restaurant-pos --public --clone
```

**方法 B：用網頁開**
1. 進 https://github.com/new
2. 設定：**Public** + Add README
3. Create → clone 下來

#### Step 2 — 加組員 + 設規範

1. **加組員為 collaborator**：repo → Settings → Collaborators → Add people
   （ Public只是「看得到」，要協作更新程式碼 (pull、push 權限) 要做 Collaborators 這一步）
2. **開 branch protection**：repo → Settings → Branches → Add rule
   - ✅ Require PR before merging
   - ✅ Require 1 approval

#### Step 3 — 第一個 commit

把組員名稱 / 暱稱和分配角色（若有）寫進 README，git commit + git push。

#### 完成 checklist

- [ ] Public repo 已開（名稱：`{組名}-{專題名稱}-{情境簡寫}`，例：`G3-project_name-restaurant_pos`）
- [ ] 寫第一版本 README
- [ ] 所有組員已加為 collaborator
- [ ] main branch protection 簡單設定（PR + 1 approve）
- [ ] 第一個 commit 進行 push（含組員名單在 README）

**交付**：repo URL 貼到 line 群組

#### ⚠️ 一般版的限制

| 風險 | 說明 |
|---|---|
| Repo owner 只有組長 | 會有誤刪的狀況 |
| 銷帳號 | 履歷指向死連結 |
| commit graph 視覺集中在組長帳號 | 其他人在 contributors 區較不顯眼 |

**降風險作法**：
- README 寫明「本 repo 為小組共同作品，組長為代管，組長也的確會有需要花較多心神和時間，所以放在組長這也算合理」
- commit 時用 `Co-authored-by:` 把貢獻歸給每人（看 03 章）
- 每人定期 fork 一份到自己帳號當備份

---

### 🚀 專業版：組織 Org 主 repo + 個人 Github 的 portfolio repo

跟 Side Project 一樣的雙軌做法

```
github.com/tir105-g3/restaurant-pos     ← 團隊的主 repo（Organization Github）
                ↑↓ 互相連結
github.com/yourname/portfolio           ← 美人的個人作品集（每人一份）
```

#### Step 1 — 開團隊 Organization Github Account

1. 進 https://github.com/account/organizations/new → 選 **Free** plan
2. Settings → Members → Invite 組員都加進來
3. 在 org 底下開 public repo（步驟跟一般版 Step 1 一樣，只是 owner 換成 org）
4. 開 branch protection（同一般版 Step 2）

#### Step 2 — 每人開個人 portfolio repo

每位組員都要做一次：

在自己 GitHub 帳號開一個 Public repo：`{your-username}/portfolio`

#### Step 3 — 兩邊互相連結

- 團隊 Repo README 加：「本專題由以下成員合作，每人 portfolio：@a @b @c @d」
- 個人 portfolio 加：「此專題的團隊 repo：[團隊 Repo 連結]」

#### 完成確認 checklist

- [ ] 已開團隊 Organization（Free plan）
- [ ] 團隊主 repo 開在 org 底下，組員都進 org
- [ ] 主 repo 已設 branch protection
- [ ] 每人都開了自己的 portfolio repo
- [ ] 個人 portfolio README 已用範本填好「我的角色 / 貢獻 / 技術棧」
- [ ] 兩邊互相連結
- [ ] 履歷只放個人 portfolio 連結（不放團隊 repo）

**交付**：團隊 repo URL + 全組組員 portfolio URL 都貼到 line 群組

#### 💎 為何這樣做

- 團隊作品共有
- 每人有自己的「面試入口」（履歷只貼一個 portfolio URL）
- portfolio 不限這個專題（side project / 學習筆記都能放）
- 不只培訓的作品集，而是當作真正的 Side Project

---

> 💡 兩種版本的共通理由：課程結束後，這個 repo 會是面試代表作。公開的話面試官可以直接看你的 PR / commit / 討論深度。

---

## 下一步

- 不熟 git 指令？看上面三份教學任一份 + 讀 [05 業界協作 SOP](05-collaboration-sop.md)
- 開好 repo 不知道做什麼？讀 [03 小組 10 階段流程](03-team-process.md)
- 選不出題目？讀 [04 痛點地圖](04-pain-points-industry-map.md)

---

← [回到 README](README.md)
