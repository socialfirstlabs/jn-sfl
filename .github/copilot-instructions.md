# Copilot Instructions for `jn-sfl`

## Maintenance requirement

- Keep this file updated whenever repository behavior, page structure, shared UI patterns, commands, or conventions change.
- Treat this file as long-lived context for future AI sessions (Copilot and similar assistants), so stale guidance should be corrected in the same change where possible.

## Build, test, and lint commands

This repository is a static HTML site and does not define build, test, or lint scripts/manifests (no `package.json`, `Makefile`, or test runner config).

- **Build:** none defined
- **Lint:** none defined
- **Test suite:** none defined
- **Single test:** not applicable (no test framework in this repo)

For local verification, serve the root directory with a static file server (for example: `python -m http.server 8000`) and open `index.html`.

## High-level architecture

- The site is composed of standalone pages at the repo root:
  - `index.html` (main landing page with most sections and anchor targets)
  - `about-us.html`
  - `blog.html`
  - `blog-first-week-tokyo.html` (sample blog detail page)
  - `contact.html`
  - `services.html`
  - `service-language-interview-coaching.html` (sample reusable service detail page)
- Each page is self-contained: Tailwind CDN setup, Tailwind theme extension, component styles, page markup, and JavaScript are all embedded directly in the HTML file.
- Shared UI blocks are duplicated across pages (not imported from partials): nav bar, footer, apply modal, and most interactive JavaScript.
- Navigation mixes dedicated pages and `index.html#...` anchors for primary marketing sections (`#japan`, `#programs`, `#services`, `#success`, etc.).
- Interactivity is vanilla JavaScript with inline event handlers:
  - apply modal open/close and submit feedback
  - mobile nav toggle behavior
  - accordion toggle behavior
  - reveal/counter animations via `IntersectionObserver`
  - simple form UX feedback (client-side only; no backend integration in this repo)

## Key repository conventions

- **Keep shared code synchronized across all HTML pages.** If you change shared tokens/behavior (Tailwind config, utility classes, modal/nav/footer markup, global JS functions), mirror the update in each page that duplicates it.
- **Preserve the Tailwind token naming scheme** used in inline config (`primary`, `accent`, `text`, `bg.off`, `border-color`) and existing reusable classes (`.container-custom`, `.section-pad`, `.btn*`, `.section-label`, `.reveal`).
- **Do not rename DOM IDs/classes used by shared JS** unless updating all references together (`navbar`, `navLinks`, `hamburger`, `applyModal`, `applyModalBackdrop`, `applyModalContent`, `.accordion-content`, `.accordion-icon`, `.stat-number`, `.reveal`).
- **Follow existing event wiring style**: handlers are referenced inline (`onclick`, `onsubmit`) and implemented as global functions in the bottom `<script>` block.
- **Asset paths are root-relative file references** for local brand assets (`JN_Logo*.png`, `hero-img.png`, `favicon.ico`) and direct external URLs for remote imagery/social links.
