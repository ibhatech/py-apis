# py-apis — Python notebook site

Runnable Jupyter notebooks demonstrating common Python modules, built into a
static site with [Jupyter Book](https://jupyterbook.org) and published to GitHub
Pages by CI. Served at **https://py-apis.ibhatech.com**.

## Adding or editing content

Drop a new `NN_name.ipynb` into this folder (or edit an existing one) and push.
The table of contents is regenerated automatically (`gen_toc.py`), so new
notebooks appear on the site with no config changes. Number the filename prefix
(`01_`, `02_`, ...) to control ordering.

## Build locally

```bash
source ~/_dj/bin/activate          # your virtual environment
pip install -r requirements.txt
python gen_toc.py                  # refresh the toc from current notebooks
jupyter-book build .
open _build/html/index.html        # macOS
```

## How it deploys

Every push to `main` runs `.github/workflows/deploy.yml`, which regenerates the
toc, executes the notebooks fresh, builds `_build/html/`, adds the `CNAME`, and
publishes to GitHub Pages. No `gh-pages` branch is used.

## One-time setup

**Repo + push**
```bash
cd ~/dev/tech-research/nb-site
rm -rf .git .DS_Store
git init -b main
git add -A
git commit -m "Initial commit: py-apis notebook site"
git remote add origin git@github.com:ibhatech/py-apis.git
git push -u origin main
```

**Enable Pages:** repo **Settings -> Pages -> Source = GitHub Actions**.

**Custom domain (`py-apis.ibhatech.com`):**
1. At your DNS provider for `ibhatech.com`, add a `CNAME` record:
   host `py-apis`  ->  target `ibhatech.github.io.`
2. In **Settings -> Pages -> Custom domain**, enter `py-apis.ibhatech.com` and save.
3. Once GitHub verifies DNS, tick **Enforce HTTPS**.

The `CNAME` file in this repo already contains the domain, so Pages keeps it set.
