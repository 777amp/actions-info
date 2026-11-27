# Deployment (GitHub Pages)

Deploy static sites or build directories to GitHub Pages (`crazy-max/ghaction-github-pages`).

## What it can do
- Push a `build_dir` to `gh-pages` (or any `target_branch` / external `repo`)
- Keep commit history (`keep_history: true`) or force-push clean snapshots
- Write a custom domain `CNAME` (`fqdn`)
- Toggle Jekyll (`jekyll: false` adds `.nojekyll`)
- Pair with GPG signing (`ghaction-import-gpg`)

## Key Inputs & Env
- **Inputs**: `build_dir` *(required)*, `target_branch` (default: `gh-pages`), `repo`, `domain`, `keep_history`, `allow_empty_commit`, `fqdn`, `jekyll`, `commit_message`, `committer`, `author`, `dry_run`, `verbose`
- **Env**: `GITHUB_TOKEN` (same repo) or `GH_PAT` (deploying to another repo)

## Examples

### Basic deploy
```yaml
permissions:
  contents: write

jobs:
  publish:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Deploy to GitHub Pages
        uses: crazy-max/ghaction-github-pages@v5
        with:
          target_branch: gh-pages
          build_dir: public
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

### Deploy with GPG-signed commits
```yaml
      - name: Import GPG key
        uses: crazy-max/ghaction-import-gpg@v6
        with:
          gpg_private_key: ${{ secrets.GPG_PRIVATE_KEY }}
          passphrase: ${{ secrets.PASSPHRASE }}
          git_user_signingkey: true
          git_commit_gpgsign: true

      - name: Deploy to GitHub Pages
        uses: crazy-max/ghaction-github-pages@v5
        with:
          target_branch: gh-pages
          build_dir: public
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
```
