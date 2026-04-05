# Richter Jones — publication site

A quiet, editorial website for Richter Jones Law (Santa Fe). Replaces the current Framer template with a Substack-first publication design.

## What's in this folder

| File | Purpose |
|---|---|
| `index.html` | Standalone working mockup. Open in any browser to preview. This is the visual source of truth. |
| `CLAUDE.md` | Project context for Claude Code. Auto-loaded on session start. Read first. |
| `DESIGN.md` | Complete design system: colors, type, components, anti-patterns. |
| `PRD.md` | Product requirements document. The "why" behind every decision. |
| `BUILD_PLAN.md` | Sprint-by-sprint execution plan for building the real site. |
| `README.md` | This file. |

## To preview the mockup

```bash
open index.html
```

Or drag the file into any browser window. No build step required.

## To start the real build with Claude Code

From this directory:

```bash
claude
```

Then paste the kickoff prompt from the bottom of this README.

## Tech stack (target)

- **Astro** static site generator
- **Substack RSS** as the content source (no CMS, no local blog)
- **Cloudflare Pages / Vercel / Netlify** for hosting
- **Plain CSS** with custom properties — no Tailwind, no UI libraries
- **Two fonts**: Spectral (serif) and Inter Tight (sans), Google Fonts

## Design principles in one breath

Warm cream paper, deep ink text, one oxblood accent. One logo instance per page. No stock photos. No fake credibility badges. No per-post pages — essays live on Substack. Austerity over decoration. Every element must justify its presence.

For the complete list of anti-patterns (things we deliberately rejected), see `DESIGN.md` section "Anti-patterns."

## Claude Code kickoff prompt

Copy and paste this into Claude Code in this directory:

> Read `CLAUDE.md`, `DESIGN.md`, `PRD.md`, and `BUILD_PLAN.md` in full before doing anything else. Do not write code yet.
>
> Then ask me the five pre-flight questions listed at the top of `BUILD_PLAN.md`.
>
> Once I answer, begin Sprint 1: scaffold the Astro project and port the `index.html` mockup into Astro components, exactly matching the visual output of the current mockup. Do not invent new design decisions. Do not add features not listed in `BUILD_PLAN.md`. If something is ambiguous, ask.
>
> At the end of Sprint 1, run `npm run dev` and show me the localhost URL so I can compare side-by-side with `index.html`.

## Contact

Brandon Jones — The Playbook
(internal project; email me if you need context on a decision)
