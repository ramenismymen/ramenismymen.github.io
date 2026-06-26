# Deploy

**Live:** https://ramenismymen.github.io/
**Repo (published site):** https://github.com/ramenismymen/ramenismymen.github.io
(That repo holds the **built** site, not the source. The source is this folder.)

## How it's deployed

GitHub Pages serves the **user site** `ramenismymen.github.io` from the `main`
branch root. We publish the contents of `dist/` (the built site) there. We use
this manual method instead of GitHub Actions because the local `gh` token doesn't
have the `workflow` scope needed to push a workflow file.

`public/.nojekyll` makes Pages serve Astro's `_astro/` folder — don't delete it.

## Redeploy after editing (copy-paste)

From this project folder:

```bash
npm run build
cd dist
git init -b main -q
git add -A
git commit -qm "Deploy"
git push -f https://github.com/ramenismymen/ramenismymen.github.io.git main
cd ..
```

It goes live in ~1 minute. (Each deploy replaces the published site — that's fine.)

## Switching to automatic deploys (optional, later)

To have it rebuild & deploy on every push instead:
1. Re-authorize the CLI with workflow permission: `gh auth refresh -s workflow`
2. Push this source repo (incl. `.github/workflows/deploy.yml`) to a GitHub repo.
3. In that repo: Settings → Pages → Source → **GitHub Actions**.

## Before changing the domain

If you ever use a custom domain or a different repo, update `site` in
`astro.config.mjs` and the URL in `public/robots.txt`, then rebuild — canonical
URLs, Open Graph, and the sitemap all derive from `site`.
