# Automatic.css + Etch — Structural Design System

A **brand-agnostic** design system that runs *parallel* to any brand design system. This layer owns **structure & behaviour**; the brand layer owns **colour, type & iconography**. Everything here is authored to drop 1:1 into **Etch (WordPress)** with **Automatic.css (ACSS) v4** — no Tailwind, native nested CSS, strict BEM, logical properties, 100% local (DSGVO).

Use this as the standard starting point for every web project, then layer a brand design system on top.

---

## 0 · What this gives you

| Page | What it's for |
| --- | --- |
| **Overview** | Entry point — links every part, system status, at-a-glance facts |
| **Styleguide** | Living component library — tokens + every block, light & dark |
| **ACSS Setup Guide** | Step-by-step ACSS dashboard configuration |
| **ACSS Dashboard Values** | Interactive ACSS-panel clone, pre-filled, click-to-copy |
| **Etch Snippets** | Copy-paste blocks with `data-etch-element`, paste straight into Etch |

---

## 1 · Production target — Etch (WordPress) + AutomaticCSS

The live site is built in **Etch for WordPress** with **AutomaticCSS (ACSS) v4** — no TailwindCSS, native nested CSS, BEM naming. This DS is authored to match exactly:

- `assets/css/automatic.css` — full ACSS v4 framework (the generated stylesheet, reference)
- `assets/css/components.css` — our BEM components (unlayered, no prefix) — paste into Etch global CSS
- `ACSS Dashboard Values` — the exact palette (HEX) + shade L/C + type/spacing values to enter in the ACSS dashboard
- `Etch Snippets` — framework-free, paste-into-Etch sections

### Load order (mirrors live WordPress + Etch)

```
@layer etch-reset      ← WordPress/Etch reset      (lowest)
@layer etch-defaults   ← Etch defaults
automatic.css          ← ACSS framework (unlayered) ← overrides the layers
fonts.css              ← font overrides (unlayered)
components.css         ← our BEM blocks (unlayered) ← final say
```

Unlayered CSS always beats `@layer`-ed CSS, so ACSS and our components override the Etch defaults with **no specificity hacks** — exactly how it behaves on the live site.

---

## 2 · Authoring rules (NON-NEGOTIABLE)

1. **Strict BEM** — `block__element--modifier`. No prefix on block names.
2. **Native CSS nesting** — `&:hover`, `& svg`, contextual nesting. No SCSS.
3. **Logical properties only** — `padding-block/inline`, `margin-*`, `inset-*`, `inline-size/block-size`, `border-start-start-radius`… (RTL-safe).
4. **Every value is a token** — `var(--…)`. Never hard-code colours/sizes. Colours come from the ACSS palette (`--primary`, `--neutral`, semantic…).
5. **100% local (DSGVO)** — fonts, icons, JS all self-hosted. No CDN / Google Fonts at runtime.
6. **Etch attributes** — `<section data-etch-element="section">`, inner wrapper `data-etch-element="container"`.
7. **Extend ACSS, don't duplicate** — build on `.btn--*`, `.section--*`, `.bg--*`, `.text--*`, `.content-width`, `.grid--*`, `--space-*`, `--text-*`.

---

## 3 · Colour scheme — contextual

ACSS resolves text / heading / button colour **contextually** from the section background utility (`.bg--ultra-light` … `.bg--ultra-dark`). The same markup adapts to light or dark with no extra classes.

The palette in this project is a **reference palette** — the brand design system replaces the values in the ACSS dashboard. Because every component references tokens (never hex), changing the palette re-themes the whole system automatically.

---

## 4 · Fonts (reference pairing)

Self-hosted, swappable. Heading = **Clash Grotesk** (variable woff2), body = native system stack. The brand layer overrides both with two custom-property changes in `assets/css/fonts.css`. No external font requests at runtime.

---

## 5 · How to use on a new project

1. Configure ACSS in the WP dashboard using **ACSS Dashboard Values** (or the **Setup Guide**).
2. Paste `components.css` into Etch's global custom CSS.
3. Build pages from **Etch Snippets** + ACSS utilities + our component classes.
4. Layer the brand design system on top (colour, type, icons).
