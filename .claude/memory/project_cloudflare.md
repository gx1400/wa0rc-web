---
name: wa0rc-web Cloudflare/Wrangler Notes
description: Cloudflare Pages deployment config, wrangler.jsonc, and .assetsignore details
type: project
---

- `wrangler.jsonc` sets `assets.directory: "."` - entire repo root is the asset directory
- `.assetsignore` (NOT `.wranglerignore`) excludes files from deployment, follows .gitignore syntax
- Currently excludes: events-upcoming.yml, events-past.yml
- Files under `.github/` are excluded automatically (dotfiles/dotfolders)
- README.md and LICENSE are excluded via .assetsignore
- Branch protection is configured on the repo
- PRs generate Cloudflare preview deployments for testing before merge
