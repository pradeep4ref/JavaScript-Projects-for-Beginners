# GitHub Pages Landing Page — Design Spec

**Date:** 2026-04-27
**Branch:** `add-index-pages-for-github-pages`

## Goal

Add a root `index.html` landing page so the repo can be served via GitHub Pages, giving visitors a single URL to browse and launch all 26 JS projects directly in the browser.

**Live URL (once Pages is enabled):** https://pradeep4ref.github.io/JavaScript-Projects-for-Beginners/

## What Gets Built

One new file: `index.html` at the repo root. No existing project files are modified.

## Layout

Responsive card grid. Each card contains:
- An emoji representing the project
- The project name
- A link to `<ProjectFolder>/index.html`

Cards lift slightly on hover with an indigo glow border. Grid reflows automatically on smaller screens via `auto-fill` with a 160px minimum column width.

## Visual Design

- **Background:** `#111827` (dark navy)
- **Cards:** `#1f2937` with `#374151` border, `#6366f1` indigo accent on hover
- **Font:** Space Grotesk (400, 600, 700) via Google Fonts CDN
- **Header:** "⚡ JavaScript Projects" h1, subtitle, badge showing project count
- **Footer:** "Pages designed by Pradeep with the help of Claude ✨" + GitHub repo link

## Projects Included (26 total)

| Emoji | Name | Folder |
|-------|------|--------|
| 🌐 | AJAX Project | `AJAX Project` |
| 💪 | BMI Calculator | `BMI` |
| 🧮 | Calculator | `Calculator` |
| 💱 | Currency Converter | `Currency Converter` |
| 🌙 | Dark / Light Mode | `Dark Light Mode` |
| 🚫 | Disable Copy Paste | `Disable Copy Paste` |
| 🐙 | Github Search | `Github Search` |
| 🎲 | Guess the Number | `Guess Number` |
| 🖼️ | Image Gallery | `Image-Gallery` |
| 🎮 | Memory Game | `Memory Game` |
| 📝 | Notes App | `Notes App` |
| 🔑 | Password Generator | `Password Generator` |
| 🔒 | Password Strength | `Password Strength` |
| 💬 | Popup | `Popup` |
| ⏳ | PreLoader | `PreLoader` |
| 📷 | QR Code Generator | `QRcode` |
| 💬 | Random Quote | `Random Quote` |
| 🌐 | Random Quote API | `Random Quote API` |
| ⭐ | Rating | `Rating` |
| ✂️ | Rock Paper Scissors | `Rock-Paper-Scissor` |
| 🗂️ | Side Navbar | `Side Navbar` |
| ⏱️ | Stopwatch | `StopWatch` |
| 🔀 | Switch Tabs | `Switch Tabs` |
| ❌ | Tic Tac Toe | `Tic Tac Toe` |
| ✅ | To-Do List | `To-Do List` |
| 🔘 | Toggle Button | `Toggle Button` |

Folder names with spaces must be URL-encoded in href attributes (e.g. `Dark%20Light%20Mode/index.html`).

## Branch & Deployment

- Work happens on branch `add-index-pages-for-github-pages` off `main`
- After push, user enables GitHub Pages: **Settings → Pages → Branch: `add-index-pages-for-github-pages` → root → Save**
- GitHub deploys within ~2 minutes; live at https://pradeep4ref.github.io/JavaScript-Projects-for-Beginners/
