---
name: wa0rc-web Design Details
description: Visual design, CSS conventions, card layout, and card order for the site
type: project
---

## Layout
- Modernized card-grid layout (merged from `modernize` branch)
- Responsive: single column on mobile, 2-column grid at 640px+
- `card-full` class spans full width; regular `card` takes one grid column
- Card order: About, Officers, Club Events, VE Testing, QSO Contacts, Contact Us

## Fonts & Colors
- Fonts: Outfit (headings), DM Sans (body), Fira Code (callsign badge)
- Color scheme: navy (#0f2440) primary, sky blue (#4a9eed) accents, amber (#f0a830) highlights
- CSS custom properties: --navy, --sky, --amber, --bg, --card-bg, etc.

## Visual Details
- Cards have hover animations (translateY, shadow) and staggered entrance animations
- Signal stripe (amber-to-sky gradient) between header and content

## Events Card Styling
- CSS classes: `event-list`, `event-item`, `event-date`, `event-detail`, `event-name`, `event-location`
- Layout mirrors the officer-list pattern (flex row, date left, name/location right)
- Event links use var(--sky) color
- Location renders as smaller muted text below event name
- Sections labeled "Upcoming" and "Past" with `events-subheading` class
