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
