# Aletheia Blog — Cognee "Best Blogs" Side Track

A standalone, static blog post explaining how Aletheia uses Cognee to make AI memory visible, auditable, and correctable.

**Blog title:** *Aletheia: The AI Assistant That Can Learn, Unlearn, and Prove It*

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The full blog post — semantic HTML, no JavaScript |
| `styles.css` | All styling — responsive, mobile-ready, no dependencies |
| `README.md` | This file |

## Open locally

Just open `index.html` in any browser:

```bash
# From the project root
start blog/index.html          # Windows
open blog/index.html           # macOS
xdg-open blog/index.html       # Linux
```

The page loads Google Fonts over the network. Everything else is self-contained.

## Publish with GitHub Pages

### Option A: Separate repo (recommended for the side-track submission)

```bash
# 1. Create a new GitHub repo (e.g. "aletheia-blog")
# 2. Copy the blog folder contents into it
cp -r blog/* /path/to/aletheia-blog/
cd /path/to/aletheia-blog
git init && git add -A && git commit -m "Aletheia blog post"
git remote add origin https://github.com/<you>/aletheia-blog.git
git push -u origin main

# 3. In the repo's Settings → Pages:
#    - Source: Deploy from a branch
#    - Branch: main
#    - Folder: / (root)
#    - Save
#
# Your blog will be live at: https://<you>.github.io/aletheia-blog/
```

### Option B: Subfolder of this repo

```bash
# In this repo's Settings → Pages:
#   - Source: Deploy from a branch
#   - Branch: main
#   - Folder: /blog
#   - Save (note: GitHub Pages folder must be / or /docs, so you may
#     need to rename blog/ to docs/ or use a GitHub Actions workflow)
```

### Option C: GitHub Actions (custom path)

Create `.github/workflows/pages.yml`:

```yaml
name: Deploy Blog
on:
  push:
    branches: [main]
    paths: [blog/**]
permissions:
  contents: read
  pages: write
  id-token: write
jobs:
  deploy:
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - uses: actions/checkout@v4
      - uses: actions/configure-pages@v4
      - uses: actions/upload-pages-artifact@v3
        with:
          path: blog
      - uses: actions/deploy-pages@v4
        id: deployment
```

## No dependencies

- No React, no build step, no Node, no npm.
- Google Fonts loaded via `<link>` — works offline with system fonts as fallback.
- Fully static HTML + CSS.

## Customization

- Update the `href="#"` on the "View Project" links with your actual GitHub repo URL.
- All colors are CSS custom properties in `:root` — easy to rebrand.
- The test results in the "Testing the claim" section reflect actual `pytest` output from July 2026. Update if you re-run.

## License

MIT — same as the main Aletheia project.
