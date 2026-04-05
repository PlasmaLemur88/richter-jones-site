# CLAUDE.md

**This file is auto-loaded by Claude Code on every session. Read it first. Read `DESIGN.md` and `BUILD_PLAN.md` before writing code.**

---

## What this is

A new marketing website for **Richter Jones**, a Santa Fe business law firm run by David Richter and Jeremy Jones. The existing site (richterjones.com) is a stock-photo-heavy Framer template that looks like every other small-firm site on the internet. We are replacing it with a quiet, editorial, blog-first publication site that positions David and Jeremy as thinkers, not service providers.

The site's entire reason for existing is to host and promote **their Substack essays**. Essays are the product. Everything else is chrome.

## Current state

`index.html` is a complete, working single-file HTML mockup. It represents the final design direction after extensive iteration. **This file is the source of truth for visual design.** Do not rebuild the design from scratch — port the existing CSS, markup, and interaction patterns into the chosen framework.

## Recommended tech stack

- **Astro** for the site framework. Content-first, ships minimal JS, handles the HTML/CSS port cleanly, has first-class RSS support.
- **Substack RSS** as the content source. No CMS. No local post bodies. Fetch feed at build time, render essay list. All essay clicks link out to Substack.
- **Cloudflare Pages** or **Vercel** for hosting. Rebuild on a daily cron + webhook on new Substack post.
- **No React, no Tailwind, no UI libraries.** The CSS in `index.html` is hand-crafted and should stay that way. Use Astro components for structure, plain CSS for styling.

If a different stack is strongly preferred, document why in a comment and check in with the user before proceeding.

## Non-negotiable constraints

These are design decisions made deliberately during iteration. **Do not undo them without explicit user permission.**

1. **One logo instance per page only.** In the nav. Nowhere else. No hero crest. No footer logo. No decorative logo placements.
2. **No stock photos anywhere.** The old site had twelve. This site has zero in the body. The only imagery allowed is (a) the NM landscape SVG backdrop in the hero, (b) optional duotone author portraits in the Writers section if the user provides them.
3. **One Substack publication, two voices.** David and Jeremy share one publication feed. Do NOT build separate "Subscribe to David" and "Subscribe to Jeremy" flows. One subscribe action, site-wide.
4. **No per-post pages.** Clicks on essays go directly to Substack. Do not build a local blog post template.
5. **No engagement stats on cards.** No like counts, comment counts, reading progress bars. We tried this and cut it.
6. **No featured/pinned essay box in the hero.** The hero is: one italic line + one subscribe button + reader count. Period.
7. **No "Top in New Mexico" or similar badges.** No fake credibility indicators.
8. **Austerity over decoration.** If you're adding something, ask: "Does cutting this make the site worse?" If the honest answer is "no," don't add it.

## Design system in one paragraph

Warm cream paper background (`#F4EFE4`), deep ink text (`#1A1714`), single oxblood accent (`#6E1E28`). Spectral serif for all reading text, Inter Tight for small-caps labels and metadata. No other fonts. One JavaScript interaction (the hover-swap in the Latest essays split reader). Full tokens and component specs in `DESIGN.md`.

## File structure (target, once built)

```
/
├── src/
│   ├── pages/
│   │   ├── index.astro          # home
│   │   ├── david.astro          # David's essay archive
│   │   ├── jeremy.astro         # Jeremy's essay archive
│   │   └── about.astro          # one-page bio + contact
│   ├── components/
│   │   ├── Nav.astro
│   │   ├── Hero.astro
│   │   ├── SplitReader.astro    # the Latest essays interaction
│   │   ├── WritersColophon.astro
│   │   └── Footer.astro
│   ├── lib/
│   │   └── substack.ts          # RSS fetch + parse
│   └── styles/
│       └── global.css           # design tokens + base styles
├── public/
│   └── (static assets)
├── astro.config.mjs
└── package.json
```

## Content sources

- **Essays**: fetched from one Substack RSS feed (URL to be provided by user). If no URL yet, use placeholder content matching the essays in `index.html`.
- **Writer bios**: static content in `src/content/writers/` or inline in component files.
- **Contact info**: static, matches footer in `index.html`.

## What NOT to do

- Do not add a newsletter signup form on the site. The subscribe button links to Substack; Substack owns the list.
- Do not add analytics without asking (user may have a preference — Plausible, Fathom, Cloudflare Web Analytics).
- Do not add a dark mode. The cream palette is the palette.
- Do not add animations beyond what exists (sticky nav blur, hover swap on essay list, smooth fade on preview panel).
- Do not add a mobile hamburger menu. The four nav links fit on mobile with tighter gaps. Test it first.
- Do not install UI libraries. No shadcn, no Headless UI, no Radix. Hand-write everything.

## Coding style

- CSS: custom properties at the top of `global.css`, BEM-ish class names as in the mockup, no preprocessor.
- Astro components: script block on top, HTML in middle, scoped `<style>` at bottom if component-specific.
- No TypeScript unless needed for the RSS parser.
- Comments are welcome for non-obvious decisions. No comments for self-evident code.

## Questions to ask the user before Sprint 1

1. Substack feed URL (or URLs if they have separate ones today).
2. Hosting preference: Cloudflare Pages, Vercel, or Netlify.
3. Domain: stay on richterjones.com or use a subdomain during development?
4. Analytics preference.
5. Do they have real photos of David and Jeremy for the Writers section (for optional duotone treatment), or should the section stay typography-only for launch?

Do not start writing code until these are answered.
