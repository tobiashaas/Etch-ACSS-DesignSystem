# Design System — Automatic.css (ACSS) + Etch

This project is a **brand-agnostic design system** that runs *parallel* to the
brand design system. This layer owns **structure & behaviour**; the brand layer
owns **colour, type & iconography**. Goal: designs port 1:1 into **Etch (WordPress)**.

## Files
- `Design System.dc.html` — living styleguide (tokens + every component)
- `ACSS Setup Guide.dc.html` — how to configure ACSS in the WP dashboard
- `Etch Snippets.dc.html` — copy-paste-ready blocks with `data-etch-element`
- `assets/css/etch-reset.css` — `@layer etch-reset` (WP/Etch reset)
- `assets/css/etch-defaults.css` — `@layer etch-defaults` (Etch defaults)
- `assets/css/automatic.css` — full ACSS v4 framework (unlayered, reference)
- `assets/css/fonts.css` — self-hosted font @font-face + family overrides
- `assets/css/components.css` — our BEM components (unlayered, no prefix)
- `assets/css/brand.css` — brand layer (unlayered, LAST): `:root` token
  overrides only (colour/type/shape). Currently a DEMO brand — replace per
  project. Never put component rules here.

## Load order (mirrors live WordPress + Etch)
`etch-reset` → `etch-defaults` (both @layer) → `automatic.css` → `fonts.css`
→ `components.css` → `brand.css` (all unlayered). Unlayered CSS beats @layer-ed
CSS, so ACSS and our components override the Etch defaults with no specificity
hacks; `brand.css` loads last and re-themes the system purely via `:root` tokens.

## Authoring rules (NON-NEGOTIABLE)
1. **Strict BEM** — `block__element--modifier`. No prefix on block names.
2. **Native CSS nesting** — `&:hover`, `& svg`, contextual nesting. No SCSS.
3. **Logical properties only** — `padding-block/inline`, `margin-*`, `inset-*`,
   `inline-size/block-size`, `border-start-start-radius`, etc. (RTL-safe.)
4. **Every value is a token** — `var(--…)`. Never hard-code colours/sizes.
   Colours come from the ACSS palette (`--primary`, `--neutral`, semantic…).
5. **100% local (DSGVO)** — fonts, icons, JS all self-hosted. No CDN/Google
   Fonts at runtime.
6. **Etch attributes** — `<section data-etch-element="section">`, inner wrapper
   `data-etch-element="container"`.
7. Build on ACSS primitives (`.btn--*`, `.section--*`, `.bg--*`, `.text--*`,
   `.content-width`, `.grid--*`, `--space-*`, `--text-*`) — extend, don't duplicate.

## Color scheme
ACSS resolves text/heading/button colour contextually from the section
background utility (`.bg--ultra-light` … `.bg--ultra-dark`). Same markup adapts.

## When building new pages here
Author as `.dc.html`. In `<helmet>`, link the five stylesheets in the order
above, then write semantic markup using ACSS utilities + our component classes.
