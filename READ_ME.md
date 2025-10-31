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


#blog更新
git add -A
git commit -m "Update layout and blog page"
git pull --rebase origin main
git push origin main

#index更新
git add -A
git commit -m "Style buttons; verify About/Contact links from index"
git push

#一般部署



🚀 想再簡化？可以設成 alias：

在終端機打：

git config --global alias.ap '!git add -A && git commit -m "update" && git push'

以後你只要輸入：
git ap

就等於自動幫你完成「add + commit + push」✨
（訊息是 "update"，你也可以改成自己的預設）