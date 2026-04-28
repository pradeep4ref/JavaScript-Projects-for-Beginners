# Unified Theme Design Spec

**Date:** 2026-04-28
**Branch:** `add-index-pages-for-github-pages` (continue on same branch)

## Goal

Apply a consistent dark theme, shared font (Space Grotesk), and shared navigation header across all 26 projects and the landing page. Replace emoji icons on the landing page with Phosphor Icons (Regular weight).

## What Gets Created / Modified

| File | Action | Responsibility |
|------|--------|---------------|
| `theme.css` | Create | CSS variables, body background, font, shared input/button/card styles |
| `index.html` (root) | Modify | Add Phosphor CDN, replace emojis with `<i>` icons, link `theme.css` |
| `<Project>/index.html` × 26 | Modify | Add `theme.css` link, Phosphor CDN script, inject shared nav header |
| `<Project>/style.css` × 26 | Modify | Remove `body` background-image, background-color, and font-family overrides — let `theme.css` own those |

**Nothing else changes.** All JS files, project layouts, Bootstrap usage, and project-specific styles (button colors, card sizes, etc.) stay untouched.

## theme.css — CSS Variables & Base Styles

```css
/* CSS custom properties — single source of truth for the palette */
:root {
  --bg-primary: #111827;
  --bg-surface: #1f2937;
  --bg-nav: #1e1b4b;
  --border: #374151;
  --accent: #6366f1;
  --accent-hover: #4f46e5;
  --text-primary: #f3f4f6;
  --text-secondary: #9ca3af;
  --text-accent: #a5b4fc;
  --font: 'Space Grotesk', sans-serif;
}

/* Google Fonts */
@import url('https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;600;700&display=swap');

body {
  background-color: var(--bg-primary);
  font-family: var(--font);
  color: var(--text-primary);
  margin: 0;
  min-height: 100vh;
}

/* Shared nav header */
.site-nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 12px 24px;
  background: var(--bg-nav);
  border-bottom: 1px solid var(--border);
  font-size: 0.85rem;
  font-weight: 600;
}

.site-nav a {
  color: var(--text-accent);
  text-decoration: none;
  display: flex;
  align-items: center;
  gap: 6px;
  transition: color 0.15s;
}

.site-nav a:hover { color: #fff; }

.site-nav .site-title {
  color: #fff;
  font-weight: 700;
}
```

## Shared Nav Header (injected into all 26 project index.html files)

```html
<!-- Phosphor Icons CDN (add to <head>) -->
<script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
<!-- Theme (add to <head>, BEFORE project's own style.css) -->
<link rel="stylesheet" href="../theme.css">

<!-- Nav header (add as first child of <body>) -->
<nav class="site-nav">
  <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
  <span class="site-title">⚡ JS Projects</span>
</nav>
```

Note: `href="../theme.css"` and `href="../index.html"` use `../` because all projects are one level deep from the repo root.

## Landing Page (root index.html) Changes

- Add Phosphor CDN script to `<head>`
- Replace each `<span class="emoji">` with `<i class="ph ph-{icon-name}">` using Regular weight
- Link `theme.css` directly (no `../` prefix — same level as root)

### Icon Mapping (landing page)

| Project | Phosphor Icon Class |
|---------|-------------------|
| AJAX Project | `ph-wifi-high` |
| BMI Calculator | `ph-person-simple-run` |
| Calculator | `ph-calculator` |
| Currency Converter | `ph-currency-circle-dollar` |
| Dark / Light Mode | `ph-moon-stars` |
| Disable Copy Paste | `ph-prohibit` |
| Github Search | `ph-github-logo` |
| Guess the Number | `ph-dice-five` |
| Image Gallery | `ph-images` |
| Memory Game | `ph-brain` |
| Notes App | `ph-note-pencil` |
| Password Generator | `ph-key` |
| Password Strength | `ph-lock-key` |
| Popup | `ph-bell-ringing` |
| PreLoader | `ph-spinner-gap` |
| QR Code Generator | `ph-qr-code` |
| Random Quote | `ph-quotes` |
| Random Quote API | `ph-cloud-arrow-down` |
| Rating | `ph-star` |
| Rock Paper Scissors | `ph-hand-fist` |
| Side Navbar | `ph-sidebar-simple` |
| Stopwatch | `ph-timer` |
| Switch Tabs | `ph-tabs` |
| Tic Tac Toe | `ph-x-square` |
| To-Do List | `ph-check-square` |
| Toggle Button | `ph-toggle-right` |

## Per-Project style.css Changes

Remove only these declarations from each project's `style.css` (let `theme.css` own them):
- `body { background-image: ... }` — remove entirely
- `body { background-color: ... }` — remove (unless it's a project-specific override needed for a sub-element)
- `body { font-family: ... }` — remove
- `body { color: ... }` — remove if it's just white/light text (theme handles it)

**Do not remove** any layout, padding, margin, or component-specific styles.

## Implementation Order

Process projects in this order to catch any structural surprises early:
1. Create `theme.css`
2. Update root `index.html` (landing page)
3. Calculator (simplest, use as template)
4. Remaining 25 projects alphabetically

## CSS Path Note

The AJAX project uses `Ajax.html` not `index.html`. Apply the same changes there.
