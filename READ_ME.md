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
# 設定 .gitignore，忽略 .DS_Store 跟 vendor/
cat <<
