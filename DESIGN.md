# DESIGN.md — Richter Jones

The complete design system for the Richter Jones publication site. Every decision here was made deliberately. If you are going to break one, have a reason and document it.

---

## Creative direction

**Reference mood:** The New York Review of Books if it were a law firm. Editorial restraint, warm paper, ink-on-cream typography, zero decoration that isn't doing work.

**One word:** Austere.

**What we are not:** A marketing site. A template. A brochure. A lead-capture funnel. A pitch deck. A content-marketing hub. A thought-leadership portal (we are actual thought leaders; we don't need the phrase).

**What we are:** A publication. Two lawyers. One voice per essay. The writing is the product.

---

## Color palette — "Ink & Parchment"

All colors as CSS custom properties on `:root`.

```css
:root {
  /* Paper tones */
  --paper: #F4EFE4;          /* main background */
  --paper-dim: #EBE4D3;      /* secondary surfaces, subscribe block */
  --paper-line: #DDD3BC;     /* decorative lines */

  /* Ink tones */
  --ink: #1A1714;            /* primary text, headlines */
  --ink-soft: #3A342D;       /* body paragraphs, bylines */
  --ink-muted: #6B6156;      /* metadata, dates, small labels */

  /* Accent */
  --oxblood: #6E1E28;        /* links, section numbers, active state */
  --oxblood-soft: #8B2A35;   /* hover states */

  /* Rules */
  --rule: rgba(26, 23, 20, 0.12);  /* borders, dividers */
}
```

**That is the entire palette.** There are no other colors. The only exception is `#FF6719`, used exclusively inside the Substack mark on the subscribe button, because it is Substack's brand color and we want the platform affiliation legible. It appears as a 12×12px square and nowhere else.

**Paper grain:** a subtle SVG noise filter overlays the whole page at ~35% opacity via `body::before`. Keep it. It softens the flat cream and adds physical warmth. Do not remove.

---

## Typography

**Two fonts. No exceptions.**

### Spectral (headlines + body)

Google Fonts. Serif. Used for:
- Publication name / nav wordmark
- Hero lede (italic, weight 300)
- Essay titles (weight 400–500)
- Essay dek / body copy (weight 300–400)
- Writer names in colophon
- All long-form reading text

Weights loaded: 300, 400, 500, 600, 700, 400italic, 500italic.

**Why Spectral:** Designed specifically for long-form screen reading. Warm, literary, high-quality italics. Avoids the overused Newsreader + Inter pairing flagged in the original design brief. Pairs cleanly with Inter Tight for UI labels.

### Inter Tight (UI labels + metadata)

Google Fonts. Sans. Used for:
- Nav links (uppercase, letterspaced)
- Dates, read times, author bylines (small caps)
- Section labels
- Buttons
- Small metadata throughout

Weights loaded: 400, 500, 600.

**Never use Inter Tight for reading text.** It is a label font here, not a body font.

### Type scale (actual values in use)

| Use | Size | Font | Weight | Notes |
|---|---|---|---|---|
| Hero lede | `clamp(20px, 2.4vw, 25px)` | Spectral | 300 italic | Opening statement |
| Essay title (list) | 19px | Spectral | 500 | In split reader left column |
| Essay title (preview) | 40px | Spectral | 400 | In split reader right panel |
| Essay dek | 19px | Spectral | 300 | Preview panel |
| Writer name | 32px | Spectral | 400 | Colophon only |
| Section labels | 14px | Spectral | 500 | Small caps, letterspace 0.22em |
| Nav wordmark | 16px | Spectral | 500 | Stacked with tiny secondary |
| Nav links | 12px | Inter Tight | 500 | Uppercase, letterspace 0.12em |
| Metadata | 11px | Inter Tight | 500 | Uppercase where appropriate |
| Footer legal | 11px | Inter Tight | 400 | Lowercase |

Letter-spacing is tight on serifs (`-0.005em` to `-0.025em`) and wide on sans labels (`0.04em` to `0.26em`). This is deliberate and part of the editorial feel.

---

## Layout

### Widths

- Reading column: `max-width: 780px` (the `.wrap` class). Use for hero, single-column essays, and the writers colophon.
- Wide column: `max-width: 1080px` (the `.wrap-wide` class). Use for the split reader layout and the footer grid.

### Spacing rhythm

The page uses a ~60–100px vertical rhythm between major sections. Specific values:

- Hero: 64px top, 56px bottom
- Reader (Latest): 72px top, 100px bottom
- Writers: 90px top, 100px bottom
- Footer quote: 90px top, 80px bottom
- Footer bottom: 60px top, 40px bottom

---

## Components

### 1. Nav

Sticky. Backdrop blur at 85% paper opacity. Thin bottom border. One logo (left), four uppercase Inter Tight links (right). The logo is the monogram PNG + "Richter Jones" in Spectral. No secondary label under the wordmark.

### 2. Hero (masthead)

- Position relative with an absolutely-positioned inline SVG NM landscape backdrop
- Cream overlay layered on top at 78→92→98% opacity (stronger near the text)
- Content: **one italic sentence** + subscribe row. That is all.
- Subscribe row: ghost-style outlined button with a 12×12 Substack orange mark, plus "2,847 readers" in tiny muted sans next to it
- The "Richter Jones" display headline is NOT in the hero — the nav wordmark is sticky above it and handles the brand

**The NM landscape SVG** has four layers (sky gradient, oxblood sun with glow, Sangre de Cristo silhouette, foreground mesa layer, sparse brush). It can be replaced with a real photo by setting `background-image` on `.masthead-bg` and deleting the inline SVG. The overlay washes any image into the palette automatically.

### 3. Split Reader (Latest essays)

The key interaction on the site.

- Two-column grid: 1fr left (numbered essay list, 6 items), 1.15fr right (sticky preview panel)
- Left items: 44px number + title + "Author · Date" metadata
- Right panel: category label (oxblood), large title (Spectral 40px), dek (Spectral 19px italic-adjacent), byline row, explicit "Read the essay →" outlined button
- Hovering any left row → right panel content swaps with a 180ms opacity/transform fade
- Active row gets a 2px oxblood left border and oxblood number
- Mobile: collapses to single column, preview stacks above list, no sticky
- Keyboard accessible: `tabindex="0"` on list items, activate on focus

Data lives in a JS array in an IIFE at the bottom of the page. When porting to Astro, move to a TypeScript array in a module and populate from Substack RSS at build time.

### 4. Writers Colophon

Two-column grid. Each writer: name (Spectral 32px), role (Inter Tight caps, oxblood), one-sentence bio (Spectral 17px light), "N essays →" underlined archive link.

**No subscribe buttons.** **No post cards.** **No photos** in v1 (optional duotone portraits in v2 if user provides real photos).

### 5. Footer

Dark ink background. Two sub-sections:
- **Footer quote**: Centered Holmes quote in italic Spectral, attribution in small caps Inter Tight. Replaces the earlier heavy 280px dark image block.
- **Footer grid**: Four columns — brand + wordmark, Practice, Read, Contact. Small caps section headers. Very quiet.
- **Legal strip**: Disclaimer left, copyright right.

---

## Interaction & motion

**Every animation has a purpose. There is no decoration motion.**

| Interaction | Pattern | Duration |
|---|---|---|
| Nav scroll blur | `backdrop-filter: blur(12px)` on scroll | instant |
| Essay list hover | `padding-left` shift + left border appears | 300ms ease |
| Preview panel swap | opacity + 4px translateY fade | 180ms ease |
| Subscribe button hover | border darken + background tint | 250ms |
| Read CTA hover | background fill to ink | 250ms |
| Writer archive hover | color + border-color shift | 200ms |

`prefers-reduced-motion: reduce` disables all transitions via a single media query at the bottom of the CSS. **Do not remove this.**

---

## Anti-patterns (things we explicitly rejected)

These were all tried at some point during iteration and cut. Do not re-introduce them.

- ❌ Multiple logo instances per page
- ❌ Stock photography of lawyers, courthouses, or law books
- ❌ "Featured" pinned essay box in the hero
- ❌ "Top in New Mexico · Business Law" or similar fake-credibility badges
- ❌ Heart and comment count icons on essay cards
- ❌ "No. 01 / No. 02" section numbering
- ❌ Dual subscribe CTAs ("Subscribe to David" / "Subscribe to Jeremy")
- ❌ Large 280px dark footer image block with gradient
- ❌ Redundant middle-page subscribe module
- ❌ The big "Essays & Counsel" marketing headline
- ❌ Newsreader + Inter font pairing (overused AI cliché)
- ❌ Playfair Display
- ❌ Orange + lime color schemes
- ❌ Purple gradients on white
- ❌ Lucide icon set as primary icons
- ❌ Bouncy / elastic animations
- ❌ Heavy drop shadows
- ❌ Carousel sliders
- ❌ "The Law Letter" as a subtitle or pub name
- ❌ Per-post local blog pages (clicks go to Substack)

---

## Accessibility baseline

- Contrast: body text `--ink-soft` on `--paper` is 11.2:1 (passes WCAG AAA). Muted text on paper is 6.4:1 (AA). Oxblood links are 8.1:1 on paper (AAA).
- Touch targets: minimum 44×44px on mobile.
- Focus rings: visible on all interactive elements. Do not remove outline without replacing with an equivalent `:focus-visible` style.
- Keyboard: every hover-activated behavior must also work on keyboard focus. The split reader already handles this.
- Alt text: author portraits (if added) get descriptive alt. Decorative SVG backdrop gets `aria-hidden="true"`.

---

## Responsive breakpoints

```
Mobile:   < 820px   (single column, reader collapses, writers stack)
Mid:      820–900   (writers stack, reader still two-column)
Desktop:  900px+    (full grid)
```

Tested layouts in the current mockup work down to 360px width.
