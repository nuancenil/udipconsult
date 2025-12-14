# UDIP Consult — Jekyll (Bilingual)

A clean, bilingual (ZH/EN) Jekyll starter ready for **GitHub Pages**. No ads, no banners.

## Quick Start
1. Create a **public repo** on GitHub (e.g., `udipconsult`).
2. Upload all files in this folder to the repo (or push via Git).
3. Go to **Settings → Pages**:
   - Source: `Deploy from a branch`
   - Branch: `main` (root)
4. Your site will be live at `https://<your-account>.github.io/udipconsult/` if the repo name is `udipconsult`.

## Local Preview (optional)
```bash
gem install bundler
bundle install
bundle exec jekyll serve
```

## Customize
- Edit `_config.yml` for title, colors, baseurl/url.
- Navigation is in `_data/nav.yml` (ZH/EN).
- Pages are at root (ZH) and `/en` (EN).
- Blog posts are in `_posts/` with `lang: zh` or `lang: en`.
- Styles in `assets/css/style.css`.

## Custom Domain (optional)
- In **Settings → Pages**, set your custom domain (e.g., `www.eudaimonia-ip.com`), then enable HTTPS.
- Add DNS: `www` → CNAME to `<your-account>.github.io` ; apex → A/ALIAS/ANAME to GitHub Pages IPs (see docs).


cd /Users/hazel/Documents/GitHub/udipconsult

# 確保在 main 分支
git checkout main

# 把現在這個專案跟遠端 main 對齊（如果你已經是乾淨狀態，這行只會同步而已）
git pull origin main

## 完整上傳 Commit 與推送到遠端（快速指南）
在修改後，依序執行以下步驟來上傳變更到遠端：

1. 檢查目前分支與工作區狀態：

```bash
git branch --show-current   # 或 git status -sb
git status
```

2. 拉取遠端最新變更（保持分支同步）

```bash
git pull --rebase origin $(git branch --show-current)
```

3. 暫存你要提交的檔案：

```bash
git add -A        # 將所有已修改/新增/刪除的檔案暫存
```

4. 提交（寫清楚、簡短的 commit 訊息）：

```bash
git commit -m "簡潔描述：做了什麼/為何做"
```

5. 推送到遠端：

- 若分支已經有對應的遠端 tracking：

```bash
git push
```

- 若是新分支或尚未設定 upstream，使用：

```bash
git push -u origin $(git branch --show-current)
```

6. 驗證遠端已收到變更：

```bash
git remote -v
git log -n 1
```

提示：在多人協作時，建議先 `git pull --rebase` 再 `git push`，遇到衝突請以編輯衝突檔案後 `git add` 並繼續 `git rebase --continue`（或視情況使用 merge）。

如果你想，我可以一併幫你把這個變更 commit 到本地（然後你決定是否要 `push`）。

## 可直接複製執行的乾淨指令
以下指令可直接複製到終端（請在執行前把 `"YOUR COMMIT MESSAGE"` 或 `feature/your-branch-name` 換成你的內容）。

情境 A — 更新現有分支（例如 `main`）：

```bash
cd /Users/hazel/Documents/GitHub/udipconsult
git checkout main
git pull --rebase origin main
git add -A
git commit -m "YOUR COMMIT MESSAGE"
git push
```

情境 B — 新分支並推上遠端：

```bash
cd /Users/hazel/Documents/GitHub/udipconsult
git checkout -b feature/your-branch-name
git add -A
git commit -m "YOUR COMMIT MESSAGE"
git push -u origin feature/your-branch-name
```

快速驗證指令：

```bash
git status
git log -n 1
git remote -v
```

提示：若發生衝突，解決衝突後執行 `git add <file>`，再使用 `git rebase --continue` 或完成合併流程。
