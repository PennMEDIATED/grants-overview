# Penn MEDIATED — Grants Overview

A static listing of the 2025 Information and Democracy Research Grants cohort, for the [Center on Media, Technology and Democracy](https://infodem.upenn.edu). Sits alongside the public `grants` page as a fuller view: every grant's summary, topics and expected outputs on the card itself.

The page ships **no JavaScript** — what you see in `index.html` is what renders.

- `index.html` — page markup, hand-authored static HTML like every other repo. Each grant is its own `<article class="card">` block — see "Editing a grant" below.
- `styles.css` — all styling (design tokens live at the top in `:root`)

Same conventions as [`about`](https://github.com/PennMEDIATED/about), [`home`](https://github.com/PennMEDIATED/home), and [`grants`](https://github.com/PennMEDIATED/grants) — shared spacing tokens, brand colors, and fonts. Pull values from `about/README.md`'s "Style guide" section rather than guessing new ones; this file only documents what's specific to this page.

## Editing a grant

There's no build step and no data files — same as every sibling repo, edit `index.html` directly.

Each grant is one `<article class="card">` in `#cardsContainer`: pillar tag, title, researchers, schools, one-line description, then two `<div class="card-meta">` blocks — Topics and Expected outputs — each a `.card-meta__label` plus a `.tag-row`. Cards carry `data-pillar`/`data-org`/`data-topics`/`data-search` attributes; nothing reads them, and `data-search` is roughly half the file's size.

A card shows its full topic list. There is no hidden content.

To add or edit a grant: copy an existing `<article class="card">...</article>` block and update the text. That is the whole procedure.

## White sections and full-bleed color

Two rules that hold across the site:

- **Colored sections run the full width of the viewport.** `.stats-band` is a top-level `<section>` carrying its own background, with a `.wrap` inside it constraining only the content. A colored section never goes inside a `.wrap` — the color would stop at 1440px. The wrap goes inside it.
- **White sections are one bordered, softly-shadowed block**, not a tinted page background and not per-item shadows. The page background is `--c-white`; the block carries `1px solid var(--border)` plus `box-shadow: 0 20px 60px rgba(13, 13, 12, 0.08)`, matching `/home`'s `.about-center__card`. Items inside the block are separated by their own `1px solid var(--border)` and nothing more.

Section headings follow the sitewide weight split: **700 on white backgrounds** (`.section-title`), **600 on colored blocks** (`.stats-band h2`).

## Spacing

Sitewide convention, same discipline as the type scale: the `--space-*` block at the top of `styles.css` is canonical and identical to `about/styles.css`. Spacing comes from those tokens, not raw px.

Section rhythm:

- **Full-width chapter sections** (`.stats-band`) carry `var(--space-1000)` (80px) top and bottom padding. A colored band with no top padding puts its heading flush against the band edge.
- **The page hero** (`header.page-header`) is `var(--space-1000)` top, `var(--space-600)` (48px) bottom — the shorter bottom because the following section supplies its own 80px.
- **The white listing block** (`section.body-section`) carries `var(--space-1000)` margins for the section break and `var(--space-800)` (64px) padding as its own inset.
- **Section title to first content** is `var(--space-300)` (24px), matching `grants-rfp`, `team-leadership` and `our-team-job-openings`. Page/hero titles use `var(--space-250)` (20px).

## Typography

Sitewide convention. The `--fs-*`/`--lh-*` block at the top of `styles.css` is the canonical copy and belongs verbatim in every page repo.

**Two families, no third.** `--f-serif` (EB Garamond) for page and section titles and for pull-quote copy; `--f-sans` (DM Sans) for everything else. There is no monospace face. Uppercase micro-labels — pillar tags and `.card-meta__label` headings — are DM Sans 700 uppercase with `letter-spacing: 0.08em`.

**Sizes come from tokens, never raw px.**

| Token | Mobile (=<480px) | Desktop (>=1440px) | Used for |
| --- | --- | --- | --- |
| `--fs-display` | 36px | 76px | full-bleed hero (not used on this page) |
| `--fs-h1` | 36px | 56px | page title |
| `--fs-h2` | 26px | 40px | section titles |
| `--fs-h3` | 20px | 24px | third-level headings |
| `--fs-lede` | 18px | 20px | intro paragraphs |
| `--fs-body` | 16px | 16px | body copy, card titles |
| `--fs-small` | 14px | 14px | card descriptions, form controls, meta |
| `--fs-small-serif` | 15px | 15px | EB Garamond at small sizes |
| `--fs-micro` | 12px | 12px | uppercase labels, tags, counts |

Page title, section title and third-level headings step 56 / 40 / 24 at desktop. The page title needs that much clearance because section titles are DM Sans 600 on saturated backgrounds while page titles are EB Garamond 600, and the heavier sans reads larger at equal size.

The top five are `clamp()` values that interpolate across the viewport, so tablet widths need no separate `@media` override. Only add a breakpoint font-size when a specific layout actually demands it.

**12px is the floor.** Nothing on the site ships smaller. EB Garamond and uppercase-with-letter-spacing both read smaller than their nominal size, which is what `--fs-small-serif` and the 12px floor exist to absorb.

**Line heights are tokens too** — `--lh-display` 1.05, `--lh-heading` 1.15, `--lh-lede` 1.26, `--lh-title` 1.3, `--lh-body` 1.55. Never set line-height in px; it breaks the fluid sizes.

## Style guide deltas from `about`

Everything not listed here (spacing scale, `--c-dark`/`--c-accent`/`--c-red`/`--c-gray`/`--c-gray-dark`/`--c-light-bg`/`--c-white`/`--c-bg`, `--c-gradient`, `--f-serif`/`--f-sans`, the `--fs-*`/`--lh-*` type scale, the 1440px/80px-responsive layout scale, the sharp-corners-except-circles rule, the sharp-corners-except-circles rule, and the box-shadow+translateY-never-border-color hover convention) is pulled straight from `about` and should stay that way.

This page defines a handful of tokens `about` doesn't need, all functional (drive dynamic UI state, not decoration):

- `--card-hover-shadow` — the card hover-shadow value.

- `--pillar-eco-bg`/`-text`, `--pillar-ai-bg`/`-text`, `--pillar-per-bg`/`-text` — the three research-pillar tag colors (also used for the purple-band dropdown tabs' accent). Drawn from the secondary color palette introduced for this page (see `grants/README.md`'s "Secondary colors" section).

## Components with no analog on `about`/`home`/`team-leadership`

This page is a data tool, not a marketing page, so several components exist here with nothing to keep in sync against:

- **Grant card** — category bar, title, researchers, affiliated schools, one-line description, then labelled Topics and Expected outputs tag rows. Hovering lifts the card `4px` and adds `--card-hover-shadow`; the border never changes color, per the sitewide convention. The first `.card-meta` carries `margin-top: auto`, so both tag groups sit together on the card's bottom edge and line up across a row regardless of description length.
- **Purple-band pillar dropdowns** — three research-area tabs (`Unpacking the Media Ecosystem` / `When AI Mediates Information` / `Persuasion and Common Ground`), one panel open at a time, each showing just that pillar's description (the grants themselves are only listed once, in the card grid below, to avoid duplicating content).

## Keeping in sync

If you change a token or component here that has an equivalent on `about`, `home`, `team-leadership`, or `grants`, check whether the change belongs there too, and vice versa — these repos duplicate CSS rather than sharing a stylesheet, so consistency is a discipline, not something enforced automatically. Tokens and components unique to this page (listed above) don't need to propagate anywhere.
