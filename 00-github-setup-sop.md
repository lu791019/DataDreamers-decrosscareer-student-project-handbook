# 00 GitHub 註冊、開通與 Fork SOP

> 沒用過 GitHub？這篇給你最快的路徑。不重寫一遍別人寫好的教學 — 我們直接指你去看最棒的。

---

## 為什麼你需要 GitHub 帳號？

| 情境 | 沒 GitHub | 有 GitHub |
|---|---|---|
| 面試 | 嘴上講過去做的事 | 「打開來給你看，這個 PR 是當時的 review」 |
| 找專案 | 找不到 | star / fork / 追蹤 trending |
| 跟組員協作 | 用 LINE / Dropbox 傳 code | 用 PR / Issue |

---

## 推薦學習資源（中文）

不用我這份從頭講，下面這 3 份社群口碑都很好，挑一份看就夠：

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

> 💡 username 想清楚再選！會跟你一輩子。建議：全小寫、用真名或暱稱、好記、不含 `_`。

### Step 2 — 本機環境（5 分鐘）

```bash
# macOS / Linux 內建 git；Windows 裝 https://git-scm.com/download/win

git --version  # 確認 git 有了

git config --global user.name "你的 GitHub username"
git config --global user.email "你註冊 GitHub 用的 email"
git config --global init.defaultBranch main
```

⚠️ email 務必跟 GitHub 一致，不然 commits 不會算到你頭上。

### Step 3 — 驗證 push 能跑（5 分鐘）

選一種：
- **HTTPS + Personal Access Token**：最簡單，照 GitHub 提示走
- **SSH key**：之後 push 不用打密碼，[官方教學](https://docs.github.com/zh/authentication/connecting-to-github-with-ssh)

驗證：
```bash
# HTTPS 直接 clone 試試
git clone https://github.com/lu791019/tibame-student-project-handbook.git

# 或 SSH
ssh -T git@github.com
```

### Step 4 — 裝 gh CLI（可選但推薦）

```bash
# macOS
brew install gh
# Windows
winget install --id GitHub.cli

gh auth login  # 一條指令登入
```

---

## 開好小組專題 repo

開 Public repo 給小組用：

```bash
# 方法 A：用 gh CLI
gh repo create your-team/G3-restaurant-pos --public --clone

# 方法 B：網頁
# 1. https://github.com/new
# 2. Public + Add README + .gitignore (Python) + MIT License
# 3. Create → clone 下來
```

### 加組員 + 設規範

1. **加組員為 collaborator**：repo → Settings → Collaborators → Add people（公開只是「能看」，要 push 還是要這一步）
2. **開 branch protection**：repo → Settings → Branches → Add rule
   - ✅ Require PR before merging
   - ✅ Require 1 approval
3. **開 labels**：`sprint-1` / `sprint-2` / `sprint-3` / `p0` / `p1` / `blocker`

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

## 最低 checklist

- [ ] 有 GitHub 帳號 + Profile 填好 + 大頭照
- [ ] 開了 2FA
- [ ] 本機 git config 設好 user.name / user.email
- [ ] 能成功 push 1 個 commit
- [ ] 看過上面 3 份教學至少 1 份

---

## 🎯 小作業：開好你們組的專題 repo

組好隊、選好情境後，把「未來 8 週的家」開出來。

- [ ] 開一個 **Public** repo（名稱：`{組名}-{情境簡寫}`，例：`G3-restaurant-pos`）
- [ ] Add README + `.gitignore`（Python） + MIT License
- [ ] 邀請組員為 collaborator
- [ ] 設 main branch protection（PR + 1 approve）
- [ ] 第一個 commit：把 4 人名字 + 角色寫進 README

**交付**：repo URL 貼到指定 channel。

> 💡 為什麼公開：8 週後這個 repo 是你的面試代表作，公開的話面試官可以直接看你的 PR / commit / 討論深度。怕 API key 外洩 → 看 03 章 secret 管理。

---

## 下一步

- 不熟 git 指令？看上面三份教學任一份 + 讀 [03 業界協作 SOP](03-collaboration-sop.md)
- 開好 repo 不知道做什麼？讀 [02 小組 10 階段流程](02-team-process.md)
- 選不出題目？讀 [04 痛點地圖](04-pain-points-industry-map.md)

---

← [回到 README](README.md)
