---
name: wa0rc-web Project Overview
description: Purpose, live URLs, tech stack, and repo structure for the WA0RC club website
type: project
---

Website for the Waypoint Amateur Radio Club (WA0RC) in Olathe, Kansas. Single-page static site showing club officers, VE testing info, QSO contact details, club events, and general contact info.

**Why:** Design philosophy is low-maintenance - only content that won't create an updating burden is included. No meeting schedules, repeater info, or other frequently-changing content.

**How to apply:** Avoid suggesting features that would require frequent manual updates. Keep the site as a single self-contained HTML file with no build process.

## Live URLs
- Production: https://wa0rc.org (also www.wa0rc.org)
- Workers dev: https://wa0rc-web.gx1400.workers.dev/
- PR branches get Cloudflare preview deployments automatically

## Tech Stack
- Single `index.html` file - no build step, no framework, no dependencies
- Hosted on Cloudflare Pages via Wrangler (`wrangler.jsonc` with `assets.directory: "."`)
- DNS managed by Cloudflare
- GitHub repo: https://github.com/gx1400/wa0rc-web (public, owned by gx1400)
- GitHub Actions for CI/CD, using a GitHub App for token auth (`secrets.APP_ID` and `secrets.APP_PRIVATE_KEY` via `actions/create-github-app-token@v3`)
- Deployment to Cloudflare triggers automatically on push to main

## Repo Structure
```
index.html                              # The website (single-page, self-contained)
wrangler.jsonc                          # Cloudflare Pages config
.assetsignore                           # Excludes non-web files from Cloudflare deployment
events-upcoming.yml                     # Upcoming club events data
events-past.yml                         # Past club events data
.github/
  workflows/
    update-dates.yml                    # Auto-updates lastUpdated and copyrightYear on push to main
    update-events.yml                   # Validates, processes, and injects events into index.html
  schemas/
    events.json                         # JSON Schema for validating event YAML files
  scripts/
    update_events.py                    # Python script that processes events and updates index.html
```
