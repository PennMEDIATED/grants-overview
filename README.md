# Penn MEDIATED — Grants Overview

An interactive dashboard of the 2025 Information and Democracy Research Grants cohort, for the [Center on Media, Technology and Democracy](https://infodem.upenn.edu). Sits alongside the public `grants` page as an internal/detailed view: search and filter the full cohort, and open a grant for its full detail (project summary, "why it matters," topics, methods, expected outputs, timeline).

- `index.html` — page markup, hand-authored static HTML like every other repo. Each grant is its own `<article class="card">` block — see "Editing a grant" below.
- `styles.css` — all styling (design tokens live at the top in `:root`)

Same conventions as [`about`](https://github.com/PennMEDIATED/about), [`home`](https://github.com/PennMEDIATED/home), and [`grants`](https://github.com/PennMEDIATED/grants) — shared spacing tokens, brand colors, and fonts. Pull values from `about/README.md`'s "Style guide" section rather than guessing new ones; this file only documents what's specific to this page.

## Editing a grant

There's no build step and no data files — same as every sibling repo, edit `index.html` directly.

Each grant is one `<article class="card">` in `#cardsContainer`, with `data-pillar`/`data-org`/`data-topics`/`data-search` attributes that the filter bar's JS reads directly off the DOM (no separate data model to keep in sync). Nested inside each card is a hidden `<div class="card-detail">` holding the extra fields the modal shows (project summary, methods, expected outputs, full timeline) — the modal just copies that block's content in when "View full details" is clicked, so a card and its modal detail are edited in the same place.

To add or edit a grant: copy an existing `<article class="card">...</article>` block (including its `.card-detail`), update the text and `data-*` attributes, and if it's a new topic or school not already covered, add a matching `<option>` to `#topicFilter` / `#orgFilter` in the filter bar.

## Style guide deltas from `about`

Everything not listed here (spacing scale, `--c-dark`/`--c-accent`/`--c-red`/`--c-gray`/`--c-gray-dark`/`--c-light-bg`/`--c-white`/`--c-bg`, `--c-gradient`, `--f-serif`/`--f-sans`/`--f-mono`, the 1440px/80px-responsive layout scale, the sharp-corners-except-circles rule, and the box-shadow+translateY-never-border-color hover convention) is pulled straight from `about` and should stay that way.

This page defines a handful of tokens `about` doesn't need, all functional (drive dynamic UI state, not decoration):

- `--pillar-eco-bg`/`-text`, `--pillar-ai-bg`/`-text`, `--pillar-per-bg`/`-text` — the three research-pillar tag colors (also used for the purple-band dropdown tabs' accent). Drawn from the secondary color palette introduced for this page (see `grants/README.md`'s "Secondary colors" section).
- `--card-hover-shadow` — shared card/tab hover-shadow value.

## Components with no analog on `about`/`home`/`team-leadership`

This page is a data tool, not a marketing page, so several components exist here with nothing to keep in sync against:

- **Filter bar** — free-text search plus pillar/school/topic dropdowns, filtering the card grid client-side by hiding/showing the static cards already in the DOM.
- **Grant card** — category bar, title, researchers, one-line description, "why it matters" callout, topic tags, timeline, "View full details" link into the modal.
- **Detail modal** — full project summary, affiliated schools, topics, methods, expected outputs, and timeline (with key milestones), read straight out of the clicked card's hidden `.card-detail` block.
- **Purple-band pillar dropdowns** — three research-area tabs (`Unpacking the Media Ecosystem` / `When AI Mediates Information` / `Persuasion and Common Ground`), one panel open at a time, each showing just that pillar's description (the grants themselves are only listed once, in the card grid below, to avoid duplicating content).

## Keeping in sync

If you change a token or component here that has an equivalent on `about`, `home`, `team-leadership`, or `grants`, check whether the change belongs there too, and vice versa — these repos duplicate CSS rather than sharing a stylesheet, so consistency is a discipline, not something enforced automatically. Tokens and components unique to this page (listed above) don't need to propagate anywhere.
