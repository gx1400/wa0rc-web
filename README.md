# wa0rc-web

Website for the Waypoint Amateur Radio Club (WA0RC) in Olathe, Kansas.

## Overview

A simple static site providing club officer information, VE testing details,
and contact info. Deployed to [Cloudflare Pages](https://pages.cloudflare.com/)
using Wrangler.

## Structure

```
index.html          - Club website (single-page)
wrangler.jsonc      - Cloudflare Pages / Wrangler configuration
.assetsignore       - Files excluded from Cloudflare Pages deployment
.github/workflows/  - GitHub Actions CI/CD
```

## Local Development

Preview the site locally with Wrangler:

```bash
npx wrangler pages dev .
```

## Deployment

Pushes to `main` trigger a GitHub Actions workflow that deploys to Cloudflare
Pages via Wrangler.

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for
details.
