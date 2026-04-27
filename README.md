# ⚡ JavaScript Projects for Beginners

A collection of 26 beginner-friendly Vanilla JavaScript projects — no frameworks, no build tools, just HTML, CSS, and JS.

**Live demo:** https://pradeep4ref.github.io/JavaScript-Projects-for-Beginners/

---

## Running Locally

### Option 1 — Python (recommended, no install needed)

```bash
git clone https://github.com/pradeep4ref/JavaScript-Projects-for-Beginners.git
cd JavaScript-Projects-for-Beginners
python3 -m http.server 8080
```

Open http://localhost:8080 in your browser. You'll see the landing page with links to all projects.

> **Why a server?** Several projects (Currency Converter, Github Search, Random Quote API, AJAX Project) make API calls that browsers block when opening files directly via `file://`. A local server avoids this.

### Option 2 — VS Code Live Server

1. Install the [Live Server extension](https://marketplace.visualstudio.com/items?itemName=ritwickdey.LiveServer)
2. Open the repo folder in VS Code
3. Click **Go Live** in the bottom status bar
4. Browser opens automatically at the landing page

### Option 3 — Node.js

```bash
npx serve .
```

---

## Opening a Single Project

Each project is self-contained in its own folder. Once the server is running, navigate to any project directly:

```
http://localhost:8080/Calculator/index.html
http://localhost:8080/To-Do%20List/index.html
```

Or open the landing page at http://localhost:8080 and click any card.

---

## Projects

| # | Project | Concepts Covered |
|---|---------|-----------------|
| 1 | AJAX Project | XMLHttpRequest, JSON parsing, API fetch |
| 2 | BMI Calculator | DOM manipulation, form input, math |
| 3 | Calculator | eval(), DOM events, string manipulation |
| 4 | Currency Converter | fetch, Promises, external API |
| 5 | Dark / Light Mode | CSS class toggle, localStorage |
| 6 | Disable Copy Paste | Event prevention, clipboard events |
| 7 | Github Search | fetch, async/await, GitHub API |
| 8 | Guess the Number | Math.random(), conditionals, game logic |
| 9 | Image Gallery | DOM traversal, dynamic rendering |
| 10 | Memory Game | timers, arrays, event listeners, game state |
| 11 | Notes App | localStorage, contenteditable, event delegation |
| 12 | Password Generator | Math.random(), string manipulation, clipboard |
| 13 | Password Strength | Regex, dynamic styling |
| 14 | Popup | CSS class toggle, overlay pattern |
| 15 | PreLoader | setTimeout, CSS animations |
| 16 | QR Code Generator | External API (qrserver.com), dynamic img src |
| 17 | Random Quote | Static arrays, Math.random() |
| 18 | Random Quote API | fetch, async/await, quotable.io API |
| 19 | Rating | Event listeners, dynamic star rendering |
| 20 | Rock Paper Scissors | Game logic, Math.random(), score tracking |
| 21 | Side Navbar | CSS transitions, class toggle |
| 22 | Stopwatch | setInterval, clearInterval, time formatting |
| 23 | Switch Tabs | Tab UI pattern, active class management |
| 24 | Tic Tac Toe | 2D game logic, win detection, turn management |
| 25 | To-Do List | localStorage, CRUD, dynamic rendering |
| 26 | Toggle Button | CSS transitions, state toggle |

---

## Project Structure

Every project follows the same pattern:

```
ProjectName/
├── index.html   # markup, loads Bootstrap via CDN
├── style.css    # project-specific styles
└── app.js       # all JavaScript (no modules, no bundler)
```

No npm, no node_modules, no build step — open and edit any file directly.

---

## License

MIT — see [LICENSE](LICENSE.md)
