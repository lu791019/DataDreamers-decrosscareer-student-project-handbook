# 00 GitHub 註冊、開通與 Fork SOP

---

## 為什麼你需要 GitHub 帳號？

| 情境 | 沒 GitHub  | 有 GitHub  |
|---|---|---|
| 面試 | 嘴上講過去做的事 | 「打開來給你看，這個 PR 是當時的 review」 |
| 找專案 | 找不到 | star、fork、追蹤 trending |
| 跟組員協作 | 用 LINE / Dropbox 傳 code | 用 PR / Issue |

---

## Part 1：註冊 GitHub 帳號

### Step 1.1 — 進入連結

https://github.com/signup

### Step 1.2 — 填註冊資料

### Step 1.3 — 驗證 + 完成

1. 收信驗證信件、點 verify
2. 帳號開通

### Step 1.4 — 設定 Profile

到 https://github.com/settings/profile，填寫


### Step 1.5 — 兩階段認證

到 https://github.com/settings/security
→ 開 2FA（用 Google Authenticator app）

## Part 2：本機環境設定

### Step 2.1 — 安裝 Git

教學：https://git-scm.com/book/zh-tw/v2/%E9%96%8B%E5%A7%8B-Git-%E5%AE%89%E8%A3%9D%E6%95%99%E5%AD%B8

參考安裝步驟：
| OS | 怎麼裝 |
|---|---|
| **macOS** | 打開 terminal → `xcode-select --install` |
| **Windows** | 下載 [Git for Windows](https://git-scm.com/download/win) |
| **Linux** | `sudo apt install git`（Ubuntu）或 `brew install git` |

驗證：
```到終端機 CLI 輸入：
git --version
# git version 2.42.x 
```

### Step 2.2 — 設定 Git 身分

```到終端機 CLI 輸入：
git config --global user.name "你的 GitHub 用戶名"
git config --global user.email "你註冊 GitHub 用的 email"
git config --global init.defaultBranch main
```

⚠️ email 務必跟 GitHub 一致，不然 commits 可能會跑掉！

### Step 2.3 — 設定 SSH（之後 push 不用打密碼）

```bash
# 1. 產生 SSH key
ssh-keygen -t ed25519 -C "你的 email"
# 一直按 Enter，passphrase 可空可不空

# 2. 加進 ssh-agent
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519

# 3. 複製公鑰
cat ~/.ssh/id_ed25519.pub
# 全選複製
```

到 https://github.com/settings/ssh/new
→ Title 填「我的筆電」
→ Key 貼上剛複製的內容
→ Add SSH key

驗證：
```bash
ssh -T git@github.com
# 看到 "Hi {username}! You've successfully authenticated"  → 成功
```

### Step 2.4 — 安裝 GitHub CLI（推薦）

```bash
# macOS
brew install gh

# Windows
winget install --id GitHub.cli

# Linux
# 看 https://github.com/cli/cli/blob/trunk/docs/install_linux.md
```

登入：
```bash
gh auth login
# 選 GitHub.com → HTTPS → Login with browser
```

---

## Part 3：Fork 手冊 Template

### Step 3.1 — 訪問手冊 repo

https://github.com/lu791019/tibame-student-project-handbook

### Step 3.2 — 右上 Fork 按鈕

點「Fork」→ 確認 Owner 是你的帳號 → 點「Create fork」

現在你有自己的 copy：`https://github.com/{你的username}/tibame-student-project-handbook`

### Step 3.3 — Clone 到本機

```bash
cd ~/code  # 或你習慣放 code 的地方
git clone git@github.com:{你的username}/tibame-student-project-handbook.git
cd tibame-student-project-handbook
```

### Step 3.4 — 試一次 push 流程

```bash
# 改個東西測試
echo "Hello GitHub" > my-first-commit.md

# 看狀態
git status

# 加進待 commit
git add my-first-commit.md

# Commit
git commit -m "test: my first commit"

# Push 到 GitHub
git push
```

訪問你的 repo 網頁 → 看到 `my-first-commit.md` → 🎉 成功

---

## Part 4： 各小組開專題用 Repo

### Step 4.1 — 用 template-repo 開新 repo

**方法 A：用 GitHub CLI（推薦）**

```bash
cd ~/code/tibame-student-project-handbook/template-repo

# 把 template-repo 內容當起點，開一個你們組的新 repo
gh repo create your-team/de-project-pos --public --source=. --remote=origin --push

# 例如組名是 G3，做餐飲 POS：
# gh repo create G3-restaurant-pos --public --source=. --push
```

**方法 B：用網頁開**

1. https://github.com/new
2. Repo name：`G3-restaurant-pos`（建議格式：`{組名}-{情境簡寫}`）
3. **Public**（業界 demo 等級的專案要公開，不然面試官看不到）
4. ✅ Add README
5. ✅ Add .gitignore → 選 Python
6. License：MIT
7. Create

開好後 clone 下來：
```bash
git clone git@github.com:{你的username}/G3-restaurant-pos.git
```

把 template-repo 的內容貼進去：
```bash
cp -r ~/code/tibame-student-project-handbook/template-repo/. .
git add .
git commit -m "chore: bootstrap from template"
git push
```

### Step 4.2 — 加組員為 collaborator

訪問你的 repo → Settings → Collaborators → Add people
→ 輸入組員 GitHub username → 邀請

組員會收信，accept 後就能 push。

### Step 4.3 — 開 branch protection（必做！）

訪問 repo → Settings → Branches → Add rule

設定 `main`：
- ✅ Require a pull request before merging
- ✅ Require approvals: 1
- ✅ Require status checks to pass before merging
- ✅ Do not allow bypassing the above settings

這樣沒人能直接 push main，必須 PR + review。

### Step 4.4 — 設定 Issue / PR labels（5 分鐘）

repo → Issues → Labels → New label，至少建：

| Label | 顏色 | 用途 |
|---|---|---|
| `sprint-1` `sprint-2` `sprint-3` | 灰 | 標 sprint |
| `priority-p0` `p1` `p2` | 紅黃綠 | 優先級 |
| `module-ingest` `pipeline` `analytics` `serve` | 藍 | 模組 |
| `schema-change` | 紫 | 改 schema 要 escalate |
| `blocker` | 深紅 | 擋住其他人 |

---

## 常見問題

### Q: Push 時被擋 "Author identity unknown"
A: 你還沒 `git config user.email` —— 回 Step 2.2

### Q: SSH 失敗 "Permission denied (publickey)"
A: 你還沒把 public key 加到 GitHub —— 回 Step 2.3

### Q: Push 被擋 "protected branch"
A: 你 4.3 設了 branch protection 對自己也生效。要走 PR 流程：
```bash
git checkout -b feature/my-change
git push -u origin feature/my-change
gh pr create  # 或上網頁開 PR
```

### Q: Fork 後想同步原 repo 的更新
A:
```bash
git remote add upstream https://github.com/lu791019/tibame-student-project-handbook.git
git fetch upstream
git checkout main
git merge upstream/main
git push
```

### Q: 不小心把 secret commit 進去
A: **立刻**：
1. revoke 那個 secret（OpenAI / GitHub / etc）
2. `git filter-repo --invert-paths --path .env`（或用 BFG Repo-Cleaner）
3. force push 覆蓋歷史
4. 重新發 secret 給組員

預防：永遠用 `.env.example`、把 `.env` 加進 `.gitignore`、commit 前看 `git diff` 是否有敏感資料。

### Q: 一台電腦兩個 GitHub 帳號（公司 + 個人）
A: 用 SSH config + 不同 key：
```
# ~/.ssh/config
Host github.com-personal
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_personal

Host github.com-work
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_work
```
然後 clone 時用 `git@github.com-personal:...`

---

## 最低 checklist（做完才算 onboard 成功）

- [ ] 有 GitHub 帳號 + Profile 填好 + 大頭照
- [ ] 開了 2FA + 存好備援代碼
- [ ] 開了 README repo（你的名片）
- [ ] 本機裝好 Git + 設好 user.name / user.email
- [ ] SSH key 設好 + 測試 `ssh -T git@github.com` 通
- [ ] 裝好 gh CLI（推薦）
- [ ] Fork 了 handbook + clone 下來
- [ ] 成功 push 過 1 次 commit
- [ ] 開了小組專題 repo + 加組員 + 設 branch protection

打勾 ≥ 8 → 你 ready 了。

---

## 🎯 小作業：開好你們組的專題 repo

組好隊、選好情境後，把「未來 8 週的家」開出來。

- [ ] 開一個 **Public** repo（名稱：`{組名}-{情境簡寫}`，例：`G3-restaurant-pos`）
- [ ] Add README + `.gitignore`（Python） + MIT License
- [ ] 邀請組員為 collaborator（公開只是「能看」，要 push 還是要這一步）
- [ ] 設 main branch protection（PR + 1 approve）
- [ ] 第一個 commit：把 4 人名字 + 角色寫進 README

**交付**：repo URL 貼到指定 channel。

> 💡 為什麼公開：8 週後這個 repo 是你的面試代表作，公開的話面試官可以直接看你的 PR / commit / 討論深度。怕 API key 外洩 → 看 03 章 secret 管理。

---

## 下一步

- 不熟 git 指令？讀 [03 業界協作 SOP](03-collaboration-sop.md)
- 開好 repo 不知道做什麼？讀 [02 小組 10 階段流程](02-team-process.md)
- 選不出題目？讀 [04 痛點地圖](04-pain-points-industry-map.md)

---

← [回到 README](README.md)
