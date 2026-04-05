# RICHTER JONES PUBLICATION SITE — PRD

**Version:** 1.0
**Author:** Brandon Jones / The Playbook
**Date:** April 2026
**Status:** Approved for build

---

## SECTION 1: THE ONE-LINER

A quiet, editorial publication site that positions a two-partner Santa Fe law firm as the voice of New Mexico business law, with all long-form content living on Substack.

---

## SECTION 2: THE PROBLEM

### Who has this problem?

```
Primary User:     New Mexico business owners, founders, and in-house counsel
                  ages 35–60 evaluating outside counsel for commercial
                  litigation, contract, and employment matters. Sophisticated
                  buyers who can smell a template website from across the room.
User Context:     Arrives via Google search, LinkedIn post, a Substack share,
                  or a direct referral. Is either (a) vetting the firm before
                  a first call or (b) reading an essay because someone sent
                  it to them.
Current Behavior: Lands on richterjones.com, sees the same stock-photo lawyer
                  template every small firm uses, decides the partners aren't
                  particularly distinguishable from any other two lawyers,
                  closes tab.
```

### What's the pain?

Law firm marketing sites are almost unreadably undifferentiated. The current site has twelve stock photos, the obligatory marble bust in a library, the "strategic representation" boilerplate, and a Holmes quote. It says nothing about how David and Jeremy actually think. Sophisticated prospects decide based on voice and judgment. The current site shows neither.

### Why now?

David and Jeremy are writing real, substantive essays on Substack and have started to build an audience (low thousands). They need a landing page that (a) directs new readers to the Substack, (b) makes the firm's positioning legible to people who arrive from Google or LinkedIn, and (c) doesn't embarrass them when a prospect clicks through from one of their posts.

### Why us?

The firm already has two genuine advantages: David and Jeremy can actually write, and they have the taste to know what a non-template site looks like. The competitors will all be on the same three Framer templates for the next five years.

---

## SECTION 3: THE VISION

### The 5-Star Experience (Expected)
Clean, readable, modern small-firm site. Loads fast, mobile-friendly, clearly lists practice areas and contact info.

### The 7-Star Experience (Magical)
The homepage reads like an editorial publication. A prospect lands on it and immediately thinks "these are lawyers who take ideas seriously." They read one essay, subscribe to the Substack, and by the time they need a commercial litigator they already trust David and Jeremy's voice. Conversion happens before the first call.

### The 11-Star Experience (Impossible but Inspiring)
The site becomes a regular read for New Mexico business operators even when they don't need a lawyer. David and Jeremy become the default names that get mentioned when someone asks "who's the good business attorney in Santa Fe?" in a Slack or a boardroom. The Substack grows into the canonical publication for thoughtful commentary on NM commercial law. Clients arrive already pre-sold because they've been reading for months.

### Ship Target
**6 stars.** Clean beats magical for v1. The writing does the magical lifting over time.

---

## SECTION 4: THE ONE EMOTION

**The Emotion: Inspired — "I want to think like this."**

A sophisticated reader lands on the site, reads the italic hero line, sees the essay titles in the split reader, hovers through a couple of previews, and feels the quiet confidence of writers who don't need to shout. The feeling is: *these people take their work seriously, and I want them in my corner when things get complicated.*

It is not the feeling of being sold to. It is the feeling of encountering a mind.

---

## SECTION 5: THE HOOK

### First Screen
Nav with one small logo. Italic sentence: *"Essays on New Mexico business, contracts, and courtrooms — from Santa Fe. By David Richter and Jeremy Jones."* Subdued subscribe button with Substack mark. A faint NM landscape behind it all, washed to the palette. Nothing else.

### Value Demonstration
Scroll once and the six most recent essay titles are visible as a numbered list with a live preview panel. The reader can browse the back catalog by moving their cursor. Total time to understand what this site is and what these lawyers think about: about 8 seconds.

### The Screenshot Moment
The split reader with a good essay title hovered, the preview panel showing a sharp dek, the "Read the essay →" button visible. It looks like a publication, not a firm website. Someone screenshots this and sends it to a colleague with "look at this law firm site."

---

## SECTION 6: CORE USER FLOW

```
1. Arrive via Google, LinkedIn share, or referral
2. Read hero line (3 seconds) — understand it's a publication
3. Hover the essay list, read 1–2 previews
4. Click "Read the essay →" and land on Substack
5. Read the essay, hit Substack's own subscribe prompt
6. Weeks or months later, need a lawyer, remember David and Jeremy
7. Return to site, click Contact, book a call
```

### The "Aha Moment"
When the preview panel swaps smoothly on hover and reveals a sharp essay title and dek. That is the 3-second moment that tells the reader "this is not a template."

**Target:** Aha within first 10 seconds on site.

---

## SECTION 7: REQUIREMENTS

### Must Have (V1)

| # | Requirement | Why Critical |
|---|-------------|--------------|
| 1 | Home page with hero, split reader (Latest essays), writers colophon, footer | The entire site is essentially this one page |
| 2 | Substack RSS integration populating essay list at build time | Latest content without manual updates |
| 3 | External links to Substack essays (no local post pages) | Substack owns the reader; keep it simple |
| 4 | Subscribe button routing to Substack subscribe page | Substack owns the list |
| 5 | Mobile responsive down to 360px | Half the traffic will be mobile |
| 6 | Contact info in footer (phone, address, LinkedIn) | The non-reading reason people visit |
| 7 | Working sticky nav with four links | Standard site navigation |
| 8 | Accessibility baseline (WCAG AA, keyboard, reduced motion) | Professional services standard |

### Should Have (V1.1)

| # | Requirement | Why Important |
|---|-------------|---------------|
| 1 | Per-writer archive pages (david, jeremy) filtered from shared feed | Lets each writer be browsed as a column |
| 2 | About page with firm history and fuller bios | For prospects evaluating the firm |
| 3 | Contact page with an actual inquiry form | For prospects ready to call |
| 4 | Duotone author portraits in writers colophon | Humanizes the page once photos exist |
| 5 | OG images and proper meta tags | For when essays get shared |

### Could Have (V2)

| # | Requirement | Why Nice |
|---|-------------|----------|
| 1 | Practice area pages (litigation, transactional, etc.) | SEO for service-specific searches |
| 2 | Search or tag filtering on the essay archive | Once there are 50+ essays |
| 3 | Newsletter archive view with grouping by year | Once archive is deep |

### Won't Have (Not this version)

| # | Excluded | Why Not Now |
|---|----------|-------------|
| 1 | Local blog post pages | Substack owns the reader and the list |
| 2 | On-site newsletter signup form | Same — Substack owns the list |
| 3 | Client portal or intake forms beyond basic contact | Not a product feature; use real tools |
| 4 | Chatbot or AI assistant | Wrong emotional register entirely |
| 5 | Dark mode | The palette is the palette |
| 6 | Testimonials or client logos | Wrong emotional register |
| 7 | Case results ticker, "wins" counter | Wrong emotional register |

---

## SECTION 8: SUCCESS METRICS

### North Star Metric

**Metric:** Substack subscribers attributed to the site
**Target:** 200 new subscribers in the first 90 days post-launch
**Why this metric:** If the site is working, readers are converting. Substack subscription is the single act that matters.

### Supporting Metrics

| Metric | Target | Timeframe |
|--------|--------|-----------|
| Home → Substack essay click-through rate | 25%+ | Month 1 |
| Contact page visits | 40+/month | Month 1 |
| Bounce rate under 60% | Yes | Month 1 |
| Average time on home page | 45s+ | Month 1 |
| Page weight under 400KB | Yes | Launch |
| Lighthouse performance score | 95+ | Launch |

### Failure Criteria

- If subscriber growth attributable to the site is under 50 in 90 days, revisit hero copy and CTA placement.
- If bounce rate is over 75%, the hero is not communicating what the site is.
- If Lighthouse performance drops below 90, something was added that shouldn't have been.

---

## SECTION 9: VALIDATION SEQUENCE

### Phase 1 — Will the writing draw people in?
**Test:** Ship v1, share across David and Jeremy's networks and LinkedIn.
**Success Signal:** 25%+ of homepage visitors click through to at least one Substack essay.
**Sample Size:** First 500 visitors.

### Phase 2 — Will readers return?
**Test:** Cohort analysis of return visitors.
**Success Signal:** 15%+ of visitors return within 30 days.
**Sample Size:** First month of traffic.

### Phase 3 — Will prospects convert?
**Test:** Track contact form submissions that reference reading the Substack.
**Success Signal:** At least 3 qualified inbound inquiries per month cite the site or the essays as source.
**Sample Size:** 90 days.

---

## SECTION 10: RISKS & ASSUMPTIONS

### Critical Assumptions

| Assumption | How We'll Validate | By When |
|------------|-------------------|---------|
| David and Jeremy will publish consistently | Track posting cadence | First 90 days |
| The essays are actually good | Reader retention and shares | Month 2 |
| Substack RSS is reliable at build time | Monitor build logs | Ongoing |
| Prospects actually care about writing when choosing a lawyer | Qualitative feedback from first clients | Month 3 |

### Known Risks

| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| Substack publishing slows down | Medium | High | Pre-write a backlog before launch |
| Site looks empty with only 3–4 essays at launch | High | Medium | Launch with 6+ essays in the feed |
| SEO weak vs. template firm sites | Medium | Medium | Strong per-essay meta on Substack, clean site structure |
| Real photos of partners never materialize for colophon | Medium | Low | Launch typography-only, add later |

### Open Questions

- [ ] Does the firm already have a Substack live, or does it need to be set up?
- [ ] One shared publication or two separate Substacks?
- [ ] Will David and Jeremy commit to a posting cadence before launch?
- [ ] Who handles the redirect from the old richterjones.com Framer site?

---

## SECTION 11: SCOPE & CONSTRAINTS

### Technical Constraints
- Platform: Web (desktop + mobile responsive)
- Stack: Astro static site + Substack RSS + Cloudflare Pages/Vercel hosting
- Integrations: Substack RSS feed (read only), optional webhook for rebuild on new post

### Business Constraints
- Timeline: Target 2–3 weeks from Sprint 1 to public launch
- Budget: Internal build (Brandon + Claude Code)
- Team: Brandon as PM/designer, Claude Code as engineer, David and Jeremy as content

### Non-Functional Requirements
- Performance: Lighthouse 95+, under 400KB page weight
- Accessibility: WCAG 2.1 AA, keyboard navigable, reduced motion support
- Security: No forms posting to the site itself beyond a static contact form (handled via Formspree, Basin, or similar)

---

## SECTION 12: OUT OF SCOPE (EXPLICIT)

1. Building a blog CMS or posting interface — Substack is the CMS
2. Client portal, intake automation, or case management
3. Online payment or retainer handling
4. Multi-language support
5. E-commerce (books, courses, templates)
6. Podcast hosting (if they start one, build separately)
7. Any "lead magnet" downloads or gated content

---

## SECTION 13: REFERENCE

### Inspiration & Prior Art

| Product/Feature | What We Like | What We'd Change |
|-----------------|--------------|------------------|
| Stratechery by Ben Thompson | Single-author publication authority, quiet design | Ours is two voices, not one |
| The Generalist by Mario Gabriele | Editorial typography, Substack-first | Ours is narrower in topic |
| NYT Opinion section | Columnist archive treatment, duotone portraits | Simpler, no paywall |
| Matt Levine's Money Stuff on Bloomberg | Voice-driven expert commentary | Ours hosts on Substack, not Bloomberg |

### Design references
- `DESIGN.md` in this repo for the full system
- `index.html` in this repo for the working mockup

---

## SIGN-OFF

| Role | Name | Approved | Date |
|------|------|----------|------|
| Product | Brandon Jones | [ ] | |
| Firm | David Richter | [ ] | |
| Firm | Jeremy Jones | [ ] | |

---

## Next Steps

1. David and Jeremy review and approve
2. Confirm Substack URL(s) and posting cadence
3. Execute `BUILD_PLAN.md` Sprint 1
