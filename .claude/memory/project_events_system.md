---
name: wa0rc-web Events System
description: How the YAML-based events system works, schema validation, and GitHub Actions workflows
type: project
---

## YAML Format
```yaml
events:
  - name: "ARRL Field Day"
    date: "2026-06-27"              # required, YYYY-MM-DD
    end_date: "2026-06-28"          # optional, for multi-day events
    url: "https://www.arrl.org/field-day"  # optional, makes name a link
    location: "Olathe Prairie Center"      # optional, shown below event name
```

## How update_events.py Works
1. Loads both YAML files (events-upcoming.yml, events-past.yml)
2. Moves any events whose date (or end_date) has passed from upcoming to past
3. Sorts upcoming soonest-first, past most-recent-first
4. Rewrites both YAML files (sorted, with all fields preserved)
5. Generates HTML and injects between `<!-- EVENTS-START -->` and `<!-- EVENTS-END -->` markers in index.html
6. Past events display is capped at 10 most recent

## Schema Validation
Event YAML files validated against `.github/schemas/events.json` using `check-jsonschema` before the update script runs. Schema enforces:
- `name` (required, non-empty string)
- `date` (required, YYYY-MM-DD pattern)
- `end_date` (optional, YYYY-MM-DD pattern)
- `url` (optional, must start with http:// or https://)
- `location` (optional, non-empty string)
- No additional properties (catches typos like `descripion`)

## GitHub Actions Workflows

### update-dates.yml
- Triggers: push to main (paths: index.html), workflow_dispatch
- Updates `const lastUpdated` and `const copyrightYear` in index.html via sed
- Commits back to main if changed

### update-events.yml
- Triggers: pull_request (paths: events-upcoming.yml, events-past.yml, .github/scripts/update_events.py), workflow_dispatch
- Commented-out daily cron schedule (`0 6 * * *`) ready to enable
- Steps: checkout PR branch or main, validate YAML, run update_events.py, commit and push if changed
- On PRs: checks out `github.head_ref` so commits go to PR branch (triggers Cloudflare preview)
- Uses GitHub App token auth (not GITHUB_TOKEN) to allow commits to trigger other workflows

## Key Workflow Notes
- `actions/create-github-app-token@v3` deprecated `app-id` in favor of `client-id`
  - update-events.yml uses new `client-id` parameter
  - update-dates.yml may still need updating to use `client-id`
- Uses `actions/checkout@v6` and `actions/setup-python@v5`
- Commit messages use conventional commits format (`chore: ...`)
