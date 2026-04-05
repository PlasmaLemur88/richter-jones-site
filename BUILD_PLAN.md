# BUILD_PLAN.md — Richter Jones

Execution plan for Claude Code. Read `CLAUDE.md` and `DESIGN.md` before Sprint 1. Each sprint ends with a working, deployable state.

---

## Pre-flight (before any sprint)

Confirm with the user:
1. Substack feed URL(s)
2. Hosting target (Cloudflare Pages, Vercel, or Netlify)
3. Node version on their local machine
4. Analytics preference (Plausible, Fathom, Cloudflare Web Analytics, or none)
5. Whether they want per-writer archive pages in v1 or v1.1

Do not begin Sprint 1 until all five are answered.

---

## Sprint 1 — Scaffold + port the mockup (1 day)

**Goal:** A working Astro project that renders the exact mockup as a homepage, with no Substack integration yet. Essay data is hardcoded.

### Tasks

1. **Initialize project**
   - `npm create astro@latest -- --template minimal --typescript strict`
   - Confirm Node + Astro versions in `package.json`
   - Set up `.gitignore`, `.nvmrc`
   - Add `prettier` with conservative defaults

2. **Port design tokens**
   - Create `src/styles/global.css`
   - Move all `:root` custom properties from the mockup verbatim
   - Move base body styles, paper grain, font imports
   - Import `global.css` in a new `src/layouts/Base.astro`

3. **Port component by component**
   - Create the following Astro components under `src/components/`:
     - `Nav.astro`
     - `Hero.astro` (including the inline NM landscape SVG)
     - `SplitReader.astro` (with the hover-swap JS as a `<script>` block)
     - `WritersColophon.astro`
     - `Footer.astro`
   - Each component's scoped `<style>` block contains ONLY that component's CSS, lifted from `index.html`
   - Verify class names match the mockup exactly

4. **Hardcode essay data temporarily**
   - In `src/data/essays.ts`, export a typed array with the six essays from the current mockup
   - `SplitReader.astro` imports this array and renders from it

5. **Build the home page**
   - `src/pages/index.astro` uses `Base` layout and composes the five components in order
   - Verify the rendered page is byte-close to `index.html` (minor whitespace OK)

6. **Verify**
   - `npm run dev` — check at localhost
   - Test hover swap interaction
   - Test mobile breakpoints (360px, 820px, 900px, 1200px)
   - Run Lighthouse, confirm 95+ performance
   - Confirm `prefers-reduced-motion` disables animations

**Exit criteria:** Astro dev server renders the mockup with identical visual output. No console errors. Lighthouse performance 95+.

---

## Sprint 2 — Substack RSS integration (half day)

**Goal:** Latest essays section populates from live Substack feed at build time.

### Tasks

1. **Write the RSS fetcher**
   - `src/lib/substack.ts`
   - Export `async function fetchEssays(feedUrl: string, limit = 6)`
   - Parse RSS XML with the `rss-parser` package or native `fetch + DOMParser`
   - Return a typed array: `{ title, url, dek, author, pubDate, category }[]`
   - `dek` comes from the RSS `<description>` or `<content:encoded>` — strip HTML, take first ~200 chars
   - `author` comes from `<dc:creator>` or a custom field; map to "David Richter" or "Jeremy Jones"
   - Handle fetch failures gracefully — fall back to cached data if build fails

2. **Wire it up**
   - In `src/pages/index.astro`, call `fetchEssays(import.meta.env.SUBSTACK_FEED_URL)` in the frontmatter
   - Pass the result to `<SplitReader essays={essays} />`
   - Delete the hardcoded `src/data/essays.ts` (or keep as fallback)

3. **Environment variables**
   - `.env.example` with `SUBSTACK_FEED_URL=`
   - Document in README

4. **Author detection**
   - If the Substack has multiple authors mixed, use `<dc:creator>` to split
   - If there's no author distinction in the feed, ask the user how they want posts attributed (a tag convention? a prefix? a naming convention?)

5. **Verify**
   - Build succeeds with real feed URL
   - Latest essays display real, current content
   - Clicking an essay opens the Substack URL in a new tab (`target="_blank" rel="noopener"`)

**Exit criteria:** `npm run build` produces a static site with real essay data baked in. Click-through to Substack works.

---

## Sprint 3 — Writer archive pages (half day)

**Goal:** `/david` and `/jeremy` pages, each showing a filtered archive of that writer's essays in a simple vertical list.

### Tasks

1. **Create page templates**
   - `src/pages/david.astro`
   - `src/pages/jeremy.astro`
   - Both use the `Base` layout
   - Both reuse `Nav` and `Footer` components

2. **Design the archive view**
   - Follow `DESIGN.md` typography and spacing rules
   - Structure: writer name (large Spectral 400), role (Inter Tight caps oxblood), bio paragraph, horizontal rule, list of all essays
   - Essay list: each item is a row with date (left), title (center, Spectral 500), dek (muted small)
   - Clickable rows → Substack
   - No split reader on archive pages; just a straightforward list

3. **Wire data**
   - Reuse `fetchEssays` from Sprint 2
   - Filter by author in the Astro frontmatter: `const davidEssays = essays.filter(e => e.author === 'David Richter')`

4. **Link from colophon**
   - Update `WritersColophon.astro` "23 essays →" links to point to `/david` and `/jeremy`
   - Generate the count dynamically from the filtered essay array

5. **Verify**
   - Both pages build and render
   - Essay counts match what's shown in colophon
   - Navigation from home → colophon → writer page → clicking an essay → Substack works end to end

**Exit criteria:** Two working archive pages with live data.

---

## Sprint 4 — Polish and pre-launch (half day)

### Tasks

1. **SEO and meta**
   - `<title>`, `<meta description>`, Open Graph tags, Twitter Card on every page
   - Canonical URLs
   - `robots.txt` and `sitemap.xml` (Astro has built-in sitemap integration)

2. **Favicons**
   - Generate from the RJ monogram: 32×32, 16×16, apple-touch-icon, safari-pinned-tab
   - Include in `<head>` of `Base.astro`

3. **Analytics**
   - Whatever the user chose in pre-flight. If Plausible or Fathom, one script tag. If Cloudflare Web Analytics, config in dashboard.

4. **Performance audit**
   - Lighthouse on all pages
   - Fix any score under 95
   - Confirm no layout shift
   - Confirm fonts load with `font-display: swap`

5. **Accessibility audit**
   - Keyboard-only walkthrough of every page
   - axe DevTools scan, fix any violations
   - Verify focus states are visible throughout

6. **Content check**
   - Proofread all static copy
   - Verify contact info in footer is correct
   - Verify LinkedIn, phone, address are live links on mobile

7. **Error states**
   - 404 page (use the same design system)
   - If Substack RSS fails at build time, show a graceful fallback ("Essays are loading — please visit us on Substack directly" with a link)

**Exit criteria:** Site is launch-ready. Lighthouse 95+ across all pages. A11y clean. All meta complete.

---

## Sprint 5 — Deploy (1–2 hours)

### Tasks

1. **Hosting setup**
   - Follow the chosen host's Astro deployment guide (Cloudflare Pages, Vercel, or Netlify)
   - Point build command to `npm run build`, output to `dist/`
   - Set `SUBSTACK_FEED_URL` as an environment variable in the hosting dashboard

2. **Rebuild automation**
   - Set up a daily cron rebuild (all three hosts support this natively)
   - Optionally: set up a webhook from Zapier or similar listening for new Substack posts → trigger rebuild

3. **Domain**
   - Staging on a temp subdomain first
   - Confirm with user before cutting over richterjones.com
   - Set up 301 redirects from old Framer site URLs if there are any to preserve

4. **Launch**
   - DNS cutover
   - Submit sitemap to Google Search Console
   - Verify live site in production

**Exit criteria:** Public site live at richterjones.com. All links resolve. Substack integration working against production.

---

## Post-launch (ongoing)

- Monitor Substack RSS reliability
- Watch analytics for first 30 days
- Collect qualitative feedback from first 10 readers
- Run a Lighthouse check weekly
- Queue Sprint 6 (About page, Contact form, practice area pages) based on actual usage data, not guesses

---

## What counts as "done"

A sprint is done when:
- Code is committed with a clear message
- `npm run build` succeeds with no warnings
- Lighthouse score is 95+ on affected pages
- A human can perform the user flows described without friction
- The user (Brandon) has seen it and signed off

A sprint is NOT done when "it works on my machine" is the main evidence.
