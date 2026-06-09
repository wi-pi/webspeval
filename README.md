# WebSP-Eval — Project Page

Static project website for **WebSP-Eval: Evaluating Web Agents on Website Security and Privacy Tasks** (PETS 2026).

## Files

```
index.html          # the page
styles.css          # styling
assets/framework.png # framework figure (Figure 1)
```

The site is fully static — no build step, no dependencies (fonts load from Google Fonts via CDN).

## Preview locally

```bash
python3 -m http.server 8000
# open http://localhost:8000
```

## Deploy on GitHub Pages

1. Create a repo and push these files to the **root** of the default branch:
   ```bash
   git init
   git add .
   git commit -m "Add WebSP-Eval project page"
   git branch -M main
   git remote add origin https://github.com/<you>/<repo>.git
   git push -u origin main
   ```
2. On GitHub: **Settings → Pages → Build and deployment**.
   - **Source:** *Deploy from a branch*
   - **Branch:** `main` / `/ (root)` → **Save**
3. The site appears at `https://<you>.github.io/<repo>/` within a minute or two.

> Tip: for a clean URL with no repo suffix, name the repo `<you>.github.io`.

## To update later

- **Dataset link:** in `index.html`, find the `id="dataset-link"` anchor and replace `href="#"` with the real URL (the label already reads "coming soon").
- **arXiv:** currently `https://arxiv.org/abs/2604.06367`.
- **Figure:** replace `assets/framework.png`.
