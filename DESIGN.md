# DESIGN.md

Source of truth: `PORTFOLIO_REDESIGN.md` §6–§8. These rules override any design skill's defaults.

## Direction: restrained neo-brutalism
Brutalist structure, calm surface. Mostly white space and black type. Borders, hard shadows, and yellow appear only on interactive or important elements.

## Tokens
```css
:root {
  --ink: #0A0A0A;
  --paper: #FAFAF7;
  --accent: #FFFE55;   /* fill only, behind black text — never yellow text on light bg */
  --muted: #5C5C5C;    /* must pass 4.5:1 on --paper */
  --line: 2px solid var(--ink);
  --shadow: 4px 4px 0 var(--ink);
  --shadow-hover: 6px 6px 0 var(--ink);
  --radius: 0px;
}
```
Dark mode optional: invert ink/paper, keep yellow fill.

## Type
- One family, two weights (Neue Montreal already in repo, or Space Grotesk / Inter Tight). Self-hosted WOFF2, Latin subset, `font-display: swap`.
- Mono accent (JetBrains Mono) only for stack tags, dates, metadata.
- Headings clamp ~2.5–5rem, tight. Body 1–1.125rem, line-height ~1.6, max ~68ch.

## Components
- **Project card:** `--line` border + `--shadow`; on hover/focus → `--shadow-hover` + 2px translate. Mono bordered chips for stack tags.
- **Buttons:** primary = yellow fill, black border, hard shadow. Secondary = transparent, black border.
- **Section header:** mono label (`01 / WORK`) above large heading.
- **Images:** black border, square corners, no blur shadows.
- **Brand:** RM monogram (`favicons/`), black + yellow. "KRiPTO9TE" is wordmark only, never the headline.

## Don'ts
No gradients, blur, glass, soft shadows, rotated cards, second accent color, emoji icons, marquees, custom cursors.

## Motion
- Native scrolling. No scroll-jacking, smooth-scroll libs, pinning, or scrubbing.
- At most ONE signature moment (hero or work intro), e.g. RM stripes slide in, or cards stagger in with hard offset.
- Everything else: reveal-on-enter (opacity + ≤16px translate, ≤300ms) or nothing.
- Prefer CSS `animation-timeline: view()` with `@supports` fallback, or a tiny IntersectionObserver. No GSAP by default.
- `prefers-reduced-motion: reduce` → no motion. Content never depends on animation finishing.

## Tech
Plain HTML + CSS + minimal vanilla JS. No jQuery/Bootstrap/animation libs. `<picture>` AVIF/WebP, explicit width/height, lazy below fold, ≤1600px. Landmarks, one h1, skip link, visible focus (hard shadow), 44px tap targets.
