# Unified Theme Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Apply a consistent dark theme (Space Grotesk font, `#111827` background, indigo accent), shared nav header, and Phosphor Icons across all 26 projects and the landing page.

**Architecture:** One new `theme.css` at the repo root is linked by every project's `index.html` before its own `style.css`. A shared `<nav class="site-nav">` block is injected as the first child of `<body>` in each project. Each project's `style.css` has its `body` background/font overrides removed so `theme.css` takes ownership. The landing page replaces emoji spans with Phosphor `<i>` tags.

**Tech Stack:** Vanilla HTML/CSS, Space Grotesk (Google Fonts via `@import` in theme.css), Phosphor Icons v2.1.1 (CDN script)

---

### Task 1: Create theme.css

**Files:**
- Create: `theme.css`

- [ ] **Step 1: Create `theme.css` at the repo root**

Write the following to `/Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners/theme.css`:

```css
@import url('https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;600;700&display=swap');

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

body {
  background-color: var(--bg-primary);
  font-family: var(--font);
  color: var(--text-primary);
  margin: 0;
  min-height: 100vh;
}

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

- [ ] **Step 2: Verify file exists**

```bash
ls -lh /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners/theme.css
```

Expected: file listed with non-zero size.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add theme.css
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: add shared theme.css with dark palette and nav styles"
```

---

### Task 2: Update the landing page (root index.html)

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Add Phosphor CDN to `<head>` and link theme.css**

In `/Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners/index.html`, replace the existing `<head>` Google Fonts links with:

```html
  <link rel="stylesheet" href="theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Remove these lines (they're now handled by `theme.css`):
```html
  <link rel="preconnect" href="https://fonts.googleapis.com">
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
  <link href="https://fonts.googleapis.com/css2?family=Space+Grotesk:wght@400;600;700&display=swap" rel="stylesheet">
```

Also remove the `body { font-family... }` and `body { background... }` declarations from the inline `<style>` block in `index.html` since `theme.css` now owns those. Keep all other styles.

- [ ] **Step 2: Replace emoji spans with Phosphor icons**

Replace every `<span class="emoji">...</span>` in the grid with `<i class="ph ph-{icon}"></i>`. Also update the `.emoji` CSS selector in the inline style to target `i` instead:

```css
.card i {
  font-size: 2.25rem;
  line-height: 1;
  color: var(--text-accent);
}
```

Full icon replacements:
```html
<!-- AJAX Project -->
<i class="ph ph-wifi-high"></i>
<!-- BMI Calculator -->
<i class="ph ph-person-simple-run"></i>
<!-- Calculator -->
<i class="ph ph-calculator"></i>
<!-- Currency Converter -->
<i class="ph ph-currency-circle-dollar"></i>
<!-- Dark / Light Mode -->
<i class="ph ph-moon-stars"></i>
<!-- Disable Copy Paste -->
<i class="ph ph-prohibit"></i>
<!-- Github Search -->
<i class="ph ph-github-logo"></i>
<!-- Guess the Number -->
<i class="ph ph-dice-five"></i>
<!-- Image Gallery -->
<i class="ph ph-images"></i>
<!-- Memory Game -->
<i class="ph ph-brain"></i>
<!-- Notes App -->
<i class="ph ph-note-pencil"></i>
<!-- Password Generator -->
<i class="ph ph-key"></i>
<!-- Password Strength -->
<i class="ph ph-lock-key"></i>
<!-- Popup -->
<i class="ph ph-bell-ringing"></i>
<!-- PreLoader -->
<i class="ph ph-spinner-gap"></i>
<!-- QR Code Generator -->
<i class="ph ph-qr-code"></i>
<!-- Random Quote -->
<i class="ph ph-quotes"></i>
<!-- Random Quote API -->
<i class="ph ph-cloud-arrow-down"></i>
<!-- Rating -->
<i class="ph ph-star"></i>
<!-- Rock Paper Scissors -->
<i class="ph ph-hand-fist"></i>
<!-- Side Navbar -->
<i class="ph ph-sidebar-simple"></i>
<!-- Stopwatch -->
<i class="ph ph-timer"></i>
<!-- Switch Tabs -->
<i class="ph ph-tabs"></i>
<!-- Tic Tac Toe -->
<i class="ph ph-x-square"></i>
<!-- To-Do List -->
<i class="ph ph-check-square"></i>
<!-- Toggle Button -->
<i class="ph ph-toggle-right"></i>
```

- [ ] **Step 3: Open in browser and verify**

```bash
cd /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners && python3 -m http.server 8080
```

Open http://localhost:8080 — verify icons render, font is Space Grotesk, dark background shows. Stop server with Ctrl+C.

- [ ] **Step 4: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add index.html
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: replace emoji with Phosphor icons on landing page"
```

---

### Task 3: Theme the Calculator (template project)

**Files:**
- Modify: `Calculator/index.html`
- Modify: `Calculator/style.css`

This project is done first as a template. The same pattern repeats for all remaining projects.

- [ ] **Step 1: Update `Calculator/index.html` — add theme + nav**

Add to `<head>` (before `style.css` link):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Remove existing Google Fonts link:
```html
  <link href="https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap" rel="stylesheet">
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Update `Calculator/style.css` — remove body overrides**

Remove these declarations from `Calculator/style.css`:
```css
body {
    background-image: url('https://png.pngtree.com/...');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    font-family: 'Roboto', sans-serif;
    color: #fff;
    height: 100vh;
}
```

- [ ] **Step 3: Verify in browser**

```bash
cd /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners && python3 -m http.server 8080
```

Open http://localhost:8080/Calculator/index.html — verify: dark background, Space Grotesk font, nav header shows "← All Projects" and "⚡ JS Projects", calculator still works.

- [ ] **Step 4: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add Calculator/index.html Calculator/style.css
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to Calculator"
```

---

### Task 4: Theme AJAX Project

**Files:**
- Modify: `AJAX Project/Ajax.html`
- Modify: `AJAX Project/Ajax.js` (no change — just noting it exists)

- [ ] **Step 1: Update `AJAX Project/Ajax.html` — add theme + nav**

Add to `<head>` (before existing stylesheet links):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body background/font overrides from existing styles in `Ajax.html`**

Find any inline `<style>` or linked CSS that sets `body { background... }` or `body { font-family... }` and remove those declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add "AJAX Project/Ajax.html"
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to AJAX Project"
```

---

### Task 5: Theme BMI

**Files:**
- Modify: `BMI/index.html`
- Modify: `BMI/style.css`

- [ ] **Step 1: Update `BMI/index.html` — add theme + nav**

Add to `<head>` (before `style.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `BMI/style.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add BMI/index.html BMI/style.css
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to BMI"
```

---

### Task 6: Theme Currency Converter

**Files:**
- Modify: `Currency Converter/index.html`
- Modify: `Currency Converter/style.css`

- [ ] **Step 1: Update `Currency Converter/index.html` — add theme + nav**

Add to `<head>` (before `style.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `Currency Converter/style.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add "Currency Converter/index.html" "Currency Converter/style.css"
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to Currency Converter"
```

---

### Task 7: Theme Dark Light Mode

**Files:**
- Modify: `Dark Light Mode/index.html`
- Modify: `Dark Light Mode/style.css`

- [ ] **Step 1: Update `Dark Light Mode/index.html` — add theme + nav**

Add to `<head>` (before `style.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `Dark Light Mode/style.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations. Note: this project toggles a `.dark` class on body — keep that CSS, just remove the default body background.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add "Dark Light Mode/index.html" "Dark Light Mode/style.css"
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to Dark Light Mode"
```

---

### Task 8: Theme Disable Copy Paste

**Files:**
- Modify: `Disable Copy Paste/index.html`
- Modify: `Disable Copy Paste/style.css`

- [ ] **Step 1: Update `Disable Copy Paste/index.html` — add theme + nav**

Add to `<head>` (before `style.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `Disable Copy Paste/style.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add "Disable Copy Paste/index.html" "Disable Copy Paste/style.css"
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to Disable Copy Paste"
```

---

### Task 9: Theme Github Search

**Files:**
- Modify: `Github Search/index.html`
- Modify: `Github Search/style.css`

- [ ] **Step 1: Update `Github Search/index.html` — add theme + nav**

Add to `<head>` (before `style.css`, after Bootstrap):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Remove the existing Poppins font link:
```html
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;400;500;600;700&display=swap" rel="stylesheet">
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `Github Search/style.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add "Github Search/index.html" "Github Search/style.css"
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to Github Search"
```

---

### Task 10: Theme Guess Number

**Files:**
- Modify: `Guess Number/index.html`
- Modify: `Guess Number/style.css`

- [ ] **Step 1: Update `Guess Number/index.html` — add theme + nav**

Add to `<head>` (before `style.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `Guess Number/style.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add "Guess Number/index.html" "Guess Number/style.css"
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to Guess Number"
```

---

### Task 11: Theme Image Gallery

**Files:**
- Modify: `Image-Gallery/index.html`
- Modify: `Image-Gallery/style.css`

- [ ] **Step 1: Update `Image-Gallery/index.html` — add theme + nav**

Add to `<head>` (before `style.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `Image-Gallery/style.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add Image-Gallery/index.html Image-Gallery/style.css
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to Image Gallery"
```

---

### Task 12: Theme Memory Game

**Files:**
- Modify: `Memory Game/index.html`
- Modify: `Memory Game/styles.css`

Note: this project uses `styles.css` (plural) and has no Bootstrap or Google Fonts — just link theme and add nav.

- [ ] **Step 1: Update `Memory Game/index.html` — add theme + nav**

Add to `<head>` (before `styles.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `Memory Game/styles.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add "Memory Game/index.html" "Memory Game/styles.css"
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to Memory Game"
```

---

### Task 13: Theme Notes App

**Files:**
- Modify: `Notes App/index.html`
- Modify: `Notes App/style.css`

- [ ] **Step 1: Update `Notes App/index.html` — add theme + nav**

Add to `<head>` (before `style.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `Notes App/style.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add "Notes App/index.html" "Notes App/style.css"
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to Notes App"
```

---

### Task 14: Theme Password Generator

**Files:**
- Modify: `Password Generator/index.html`
- Modify: `Password Generator/style.css`

- [ ] **Step 1: Update `Password Generator/index.html` — add theme + nav**

Add to `<head>` (before `style.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `Password Generator/style.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add "Password Generator/index.html" "Password Generator/style.css"
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to Password Generator"
```

---

### Task 15: Theme Password Strength

**Files:**
- Modify: `Password Strength/index.html`
- Modify: `Password Strength/style.css`

- [ ] **Step 1: Update `Password Strength/index.html` — add theme + nav**

Add to `<head>` (before `style.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `Password Strength/style.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add "Password Strength/index.html" "Password Strength/style.css"
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to Password Strength"
```

---

### Task 16: Theme Popup

**Files:**
- Modify: `Popup/index.html`
- Modify: `Popup/style.css`

- [ ] **Step 1: Update `Popup/index.html` — add theme + nav**

Add to `<head>` (before `style.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `Popup/style.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add Popup/index.html Popup/style.css
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to Popup"
```

---

### Task 17: Theme PreLoader

**Files:**
- Modify: `PreLoader/index.html`
- Modify: `PreLoader/style.css`

- [ ] **Step 1: Update `PreLoader/index.html` — add theme + nav**

Add to `<head>` (before `style.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `PreLoader/style.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add PreLoader/index.html PreLoader/style.css
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to PreLoader"
```

---

### Task 18: Theme QR Code Generator

**Files:**
- Modify: `QRcode/index.html`
- Modify: `QRcode/style.css`

- [ ] **Step 1: Update `QRcode/index.html` — add theme + nav**

Add to `<head>` (before `style.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Remove existing Google Fonts link if present:
```html
  <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600&display=swap" rel="stylesheet">
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `QRcode/style.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add QRcode/index.html QRcode/style.css
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to QR Code Generator"
```

---

### Task 19: Theme Random Quote

**Files:**
- Modify: `Random Quote/index.html`
- Modify: `Random Quote/style.css`

- [ ] **Step 1: Update `Random Quote/index.html` — add theme + nav**

Add to `<head>` (before `style.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `Random Quote/style.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add "Random Quote/index.html" "Random Quote/style.css"
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to Random Quote"
```

---

### Task 20: Theme Random Quote API

**Files:**
- Modify: `Random Quote API/index.html`
- Modify: `Random Quote API/style.css`

- [ ] **Step 1: Update `Random Quote API/index.html` — add theme + nav**

Add to `<head>` (before `style.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `Random Quote API/style.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add "Random Quote API/index.html" "Random Quote API/style.css"
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to Random Quote API"
```

---

### Task 21: Theme Rating

**Files:**
- Modify: `Rating/index.html`
- Modify: `Rating/style.css`

- [ ] **Step 1: Update `Rating/index.html` — add theme + nav**

Add to `<head>` (before `style.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `Rating/style.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add Rating/index.html Rating/style.css
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to Rating"
```

---

### Task 22: Theme Rock Paper Scissors

**Files:**
- Modify: `Rock-Paper-Scissor/index.html`
- Modify: `Rock-Paper-Scissor/style.css`

- [ ] **Step 1: Update `Rock-Paper-Scissor/index.html` — add theme + nav**

Add to `<head>` (before `style.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `Rock-Paper-Scissor/style.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add Rock-Paper-Scissor/index.html Rock-Paper-Scissor/style.css
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to Rock Paper Scissors"
```

---

### Task 23: Theme Side Navbar

**Files:**
- Modify: `Side Navbar/index.html`
- Modify: `Side Navbar/styles.css`

Note: uses `styles.css` (plural) and `script.js`.

- [ ] **Step 1: Update `Side Navbar/index.html` — add theme + nav**

Add to `<head>` (before `styles.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `Side Navbar/styles.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add "Side Navbar/index.html" "Side Navbar/styles.css"
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to Side Navbar"
```

---

### Task 24: Theme Stopwatch

**Files:**
- Modify: `StopWatch/index.html`
- Modify: `StopWatch/style.css`

- [ ] **Step 1: Update `StopWatch/index.html` — add theme + nav**

Add to `<head>` (before `style.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `StopWatch/style.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add StopWatch/index.html StopWatch/style.css
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to Stopwatch"
```

---

### Task 25: Theme Switch Tabs

**Files:**
- Modify: `Switch Tabs/index.html`
- Modify: `Switch Tabs/style.css`

- [ ] **Step 1: Update `Switch Tabs/index.html` — add theme + nav**

Add to `<head>` (before `style.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `Switch Tabs/style.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add "Switch Tabs/index.html" "Switch Tabs/style.css"
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to Switch Tabs"
```

---

### Task 26: Theme Tic Tac Toe

**Files:**
- Modify: `Tic Tac Toe/index.html`
- Modify: `Tic Tac Toe/style.css`

- [ ] **Step 1: Update `Tic Tac Toe/index.html` — add theme + nav**

Add to `<head>` (before `style.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `Tic Tac Toe/style.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add "Tic Tac Toe/index.html" "Tic Tac Toe/style.css"
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to Tic Tac Toe"
```

---

### Task 27: Theme To-Do List

**Files:**
- Modify: `To-Do List/index.html`
- Modify: `To-Do List/style.css`

- [ ] **Step 1: Update `To-Do List/index.html` — add theme + nav**

Add to `<head>` (before `style.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `To-Do List/style.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add "To-Do List/index.html" "To-Do List/style.css"
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to To-Do List"
```

---

### Task 28: Theme Toggle Button

**Files:**
- Modify: `Toggle Button/index.html`
- Modify: `Toggle Button/styles.css`

Note: uses `styles.css` (plural) and `script.js`.

- [ ] **Step 1: Update `Toggle Button/index.html` — add theme + nav**

Add to `<head>` (before `styles.css`):
```html
  <link rel="stylesheet" href="../theme.css">
  <script src="https://unpkg.com/@phosphor-icons/web@2.1.1/src/index.js"></script>
```

Add as **first child of `<body>`**:
```html
  <nav class="site-nav">
    <a href="../index.html"><i class="ph ph-arrow-left"></i> All Projects</a>
    <span class="site-title">⚡ JS Projects</span>
  </nav>
```

- [ ] **Step 2: Remove body overrides from `Toggle Button/styles.css`**

Remove any `body { background-... }`, `body { font-family: ... }`, `body { color: ... }` declarations.

- [ ] **Step 3: Commit**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners add "Toggle Button/index.html" "Toggle Button/styles.css"
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners commit -m "feat: apply unified theme to Toggle Button"
```

---

### Task 29: Push all changes

- [ ] **Step 1: Push branch to GitHub**

```bash
git -C /Users/pmoganti/Pradeep/Claude/JavaScript-Projects-for-Beginners push origin add-index-pages-for-github-pages
```

Expected: all commits pushed, no errors.

- [ ] **Step 2: Verify on GitHub Pages**

Wait ~2 minutes then open https://pradeep4ref.github.io/JavaScript-Projects-for-Beginners/ — verify Phosphor icons show on landing page, click a project, verify nav header appears with "← All Projects" link, dark background shows, Space Grotesk font is applied.
