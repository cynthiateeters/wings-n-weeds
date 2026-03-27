# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Writing style

No em dashes ("—") in any content, copy, or code comments. Use commas or periods instead.

## Commands

```bash
bun run dev      # dev server at localhost:4321
bun run build    # production build to dist/
bun run preview  # preview the dist/ build locally
```

No test suite or linter configured.

## Deployment

Manual workflow. Do not auto-deploy.

1. `gh repo create wings-n-weeds --public` + push (first time)
2. `netlify deploy --prod` to deploy to butterfly-wings.netlify.app

## Architecture

Astro 6 static site. Two pages + a content collection:

- `src/pages/index.astro`: landing page (hero, why monarchs, meet the team, CTA)
- `src/pages/log/index.astro`: Field Notes listing, sorted newest-first
- `src/pages/log/[...slug].astro`: individual post, rendered from content collection
- `src/layouts/Base.astro`: shared layout, Google Fonts, nav, footer, CSS import
- `src/styles/global.css`: all styles via CSS custom properties (no Tailwind)
- `src/content.config.ts`: Astro 6 content layer config (uses `glob` loader, NOT legacy `src/content/config.ts`)
- `src/content/posts/*.md`: Field Notes posts; frontmatter: `title`, `date`, `description`, `author?`, `tags?`

Static assets (images) live in `public/images/` and are referenced as `/images/filename`.
Source copies of the same images also live in `src/images/`. Keep both in sync when adding new assets.

## Design system

All colors are HSL custom properties defined in `global.css`. Key tokens:

| Property           | Use                         |
| ------------------ | --------------------------- |
| `--color-bg`       | Page background (cream)     |
| `--color-monarch`  | Primary CTA / buttons       |
| `--color-milkweed` | Secondary / headings accent |
| `--color-card`     | Card backgrounds            |
| `--color-peach`    | Circle backgrounds, borders |
| `--color-charcoal` | Body text and headings      |

Fonts: **Quicksand** (headings, 600/700) and **Nunito** (body, 400/600) loaded via Google Fonts in `Base.astro`.

## Adding a Field Notes post

Drop a `.md` file in `src/content/posts/` with this frontmatter. No code changes needed.

```yaml
---
title: "Post title"
date: YYYY-MM-DD
description: "One-sentence summary shown in the listing."
author: "Cynthia" # optional
tags: ["tag"] # optional
---
```

Inline `<figure>` HTML works in post body for images. Images go in `public/images/`.

## Content decisions

- The how-to guide (cage section, etc.) is deferred. It will ship as a future Field Note once the season is underway.
- Full project context (copy, branding, design decisions) is stored in memory-keeper under channels prefixed `ww-`. Pull those before making content changes.
