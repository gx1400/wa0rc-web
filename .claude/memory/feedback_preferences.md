---
name: wa0rc-web Preferences and Conventions
description: User preferences for responses and project conventions to follow
type: feedback
---

Never use em-dashes (--) in responses; use plain hyphens (-) instead.

**Why:** User preference established in prior claude.ai conversations.

**How to apply:** Always use plain hyphens in all text responses and commit messages for this project.

---

Keep the site low-maintenance - avoid suggesting content that requires frequent manual updates.

**Why:** The club doesn't want to burden maintainers with stale content.

**How to apply:** When proposing new features or content sections, evaluate whether they'd need ongoing updates. Default to rejecting such ideas or finding a way to automate them.

---

The site must remain a single self-contained HTML file with no build process, no npm, no bundler.

**Why:** Simplicity is a core design goal. No framework, no dependencies.

**How to apply:** Never suggest introducing a build step, package manager, or JS framework.
