# Horizon Capital — Agent Rules

## Project Overview
Static vanilla HTML/CSS/JS landing page for Horizon Capital Real Estate (Cleveland, OH).
Zero dependencies, no build step. Deployed via GitHub Pages to `horizoncapitalassets.com`.

## Dev Server
```
npx serve -p 3000 .
```
Already configured in `.claude/launch.json`. No compilation or bundling required.

## File Structure
```
index.html        # Single-page markup — all sections live here
css/styles.css    # All styles — BEM classes, CSS custom properties
js/main.js        # Intentionally minimal — one comment, no logic
assets/           # Images: hero-bg.jpg, og-image.jpg, logo (2.png), etc.
```
Do not create additional HTML pages, CSS files, or JS files unless explicitly asked.

## Code Style

### HTML
- Use semantic tags: `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`
- Preserve all `<meta>`, Open Graph, Twitter Card, and JSON-LD structured data tags
- Preserve `aria-label` and `aria-hidden` attributes
- Anchor navigation via `#about` and `#contact` — keep IDs stable

### CSS
- Follow BEM naming: `.block__element--modifier`
  - Examples: `.header__inner`, `.hero__bg`, `.about__title`
- Use CSS custom properties for all colors, font, and transitions — never hardcode values
- No inline styles
- No CSS frameworks (no Bootstrap, Tailwind, etc.)
- Use `clamp()` for fluid typography, not media-query font overrides

### JavaScript
- Keep `main.js` minimal — the site requires almost no JS
- No npm packages, no bundlers, no frameworks
- Smooth scroll is handled via CSS (`scroll-behavior: smooth`)

## Design Tokens (CSS Custom Properties)
```css
--color-primary:      #2A7A7B   /* teal — CTAs, accents */
--color-secondary:    #7AAFB0   /* lighter teal — decorative rules, hover */
--color-bg:           #ffffff
--color-dark:         #141414   /* contact section background */
--color-text:         #1A1A1A
--color-text-muted:   #6B6B6B
--transition:         0.25s ease
--font:               'Inter', system-ui, sans-serif
```
Always reference these variables; do not introduce new color values without updating `:root`.

## Mobile-First Design
- Always design and build for mobile first, then enhance for larger screens
- Base styles apply to mobile; use `min-width` media queries to layer desktop styles
- Every new component or element must be functional and visually complete on small screens before adding desktop-specific rules
- Test layout at 375px (iPhone) and 768px (tablet) before considering desktop done

## Responsive Breakpoints
- `860px` — nav hides, grid stacks to single column
- `540px` — tighter padding, smaller type floor
- Use `clamp(min, preferred, max)` for fluid sizing across breakpoints

## SEO & Accessibility
- Do not remove or alter the JSON-LD `<script type="application/ld+json">` block
- Do not remove canonical, OG, or Twitter meta tags
- Keep `robots.txt` and `sitemap.xml` accurate if URLs change
- Images used for content must have descriptive `alt` text

## Performance
- Prefer appropriately sized images — avoid serving large images for small display sizes
- Use modern formats (WebP) where possible, with JPEG/PNG fallback
- Lazy-load images below the fold (`loading="lazy"`)
- Avoid large, unoptimised assets in `/assets/`

## Browser Compatibility
- Prefer widely supported CSS and JS features over cutting-edge ones with partial support
- Check Can I Use before using any newer CSS property or JS API
- Avoid features that require prefixes or polyfills unless there is no practical alternative
- `clamp()`, CSS Grid, Flexbox, and custom properties are all safe to use

## What to Avoid
- Build tools (Webpack, Vite, Parcel, etc.)
- CSS preprocessors (Sass, Less)
- JavaScript frameworks or libraries (React, Vue, Alpine, jQuery)
- Adding a `package.json` or `node_modules`
- Removing the `llms.txt` file
- Force-pushing or squashing the `main` branch history

## Git Workflow

### Branching
- Every task starts on a new branch off `main`
- Branch names use a prefix matching the work type:
  - `feature/feature-name` — new features
  - `bugfix/relevant-fix-name` — bug fixes
  - `hotfix/relevant-fix-name` — urgent production fixes
  - `update/what-is-updated` — content, copy, or style updates
  - `refactor/what-is-refactored` — restructuring without behaviour change
  - `chore/task-name` — non-functional tasks (config, docs, cleanup)
- Never commit directly to `main`

### Commit Messages
- Keep messages short and direct — the diff already shows what changed
- Format: `<verb> <subject>` (e.g. `update hero headline`, `fix mobile nav padding`)
- No bullet lists, no "this commit", no over-explanation

## Deployment
Pushing to `main` automatically deploys via GitHub Pages.
The custom domain is set in the `CNAME` file — do not delete or modify it.
