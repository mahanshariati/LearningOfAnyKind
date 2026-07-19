# mdBook Visual Overhaul Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Transform the `books/` directory into a polished, browsable online book using mdBook without modifying any existing `.md` content.

**Architecture:** Add `book.toml` config pointing at `books/` as source, create `SUMMARY.md` for navigation, customize theme via `theme/css/general.css`, optionally add GitHub Actions deploy workflow.

**Tech Stack:** mdBook (Rust), custom CSS, GitHub Pages

---

### Task 1: Install mdBook

**Files:** (none — system installation)

- [ ] **Install Rust and mdBook**

Run:
```bash
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
source "$HOME/.cargo/env"
cargo install mdbook
```

Verify:
```bash
mdbook --version
```

Expected: `mdbook v0.4.x`

- [ ] **Commit** (no code changes, but note the tool is now available)

---

### Task 2: Create mdBook Configuration

**Files:**
- Create: `LearningOfAnyKind/book.toml`

- [ ] **Create `book.toml`**

Write to `LearningOfAnyKind/book.toml`:

```toml
[book]
title = "Learning of Any Kind"
language = "en"

[build]
build-dir = "book"
create-missing = false

[output.html]
site-url = "/LearningOfAnyKind/"
no-section-label = true
git-repository-url = "https://github.com/atrovan/LearningOfAnyKind"
edit-url-template = "https://github.com/atrovan/LearningOfAnyKind/edit/main/books/{path}"

[output.html.theme]
theme = "theme"
```

- [ ] **Commit**

```bash
git add LearningOfAnyKind/book.toml
git commit -m "feat: add mdBook configuration"
```

---

### Task 3: Create SUMMARY.md (Table of Contents)

**Files:**
- Create: `LearningOfAnyKind/books/SUMMARY.md`

- [ ] **Create `SUMMARY.md`**

Write to `LearningOfAnyKind/books/SUMMARY.md`:

```markdown
# Summary

- [Fundamentals of Software Engineering](./FundamentalOfSoftwareEngineering.md)
- [Hands-On Software Engineering with Golang](./HandsOnSofwareEngineeringWithGolang.md)
- [Learning Go](./LearningGo_AnIdiomaticApproachToRealWorldGoProgramming.md)
- [LPIC-1](./LPIC-1.MD)
- [Python Programming: An Introduction to CS](./PythonProgrammingAnIntroductionToComputerScience.md)
- [Unit Testing](./UnitTesting.md)
```

Note: The LPIC-1 file uses `.MD` (uppercase) extension — mdBook handles this fine.

- [ ] **Commit**

```bash
git add LearningOfAnyKind/books/SUMMARY.md
git commit -m "feat: add mdBook table of contents"
```

---

### Task 4: Build and Verify mdBook Works

**Files:** (none — verification step)

- [ ] **Run initial build**

```bash
cd /home/atrovan/Workspace/PersonalGitHub/LearningOfAnyKind
mdbook build
```

Expected: No errors. Output goes to `./book/` directory.

- [ ] **Verify book files exist**

```bash
ls -la book/
```

Expected: `index.html`, `*.html` files per chapter, `css/`, `fonts/`, `searcher.js`, etc.

- [ ] **Commit build output**

```bash
git add book/
git commit -m "chore: add initial mdBook build output"
```

---

### Task 5: Create Custom CSS Theme

**Files:**
- Create: `LearningOfAnyKind/theme/css/general.css`

- [ ] **Create `theme/css/general.css`**

Write to `LearningOfAnyKind/theme/css/general.css`:

```css
:root {
  --bg: #faf8f5;
  --fg: #2d2d2d;
  --title-color: #1a1a1a;
  --sidebar-bg: #f5f0eb;
  --sidebar-fg: #3a3a3a;
  --sidebar-active: #c0392b;
  --sidebar-active-bg: #ede4d9;
  --link-color: #c0392b;
  --link-hover: #e74c3c;
  --code-bg: #f5f0eb;
  --code-fg: #2d2d2d;
  --quote-bg: #f0ebe4;
  --quote-border: #c0392b;
  --table-border: #e0d6cc;
  --table-alt-bg: #f5f0eb;
  --heading-color: #1a1a1a;
  --accent: #c0392b;
  --accent-light: #e8d5cc;
}

body {
  font-family: "Georgia", "Palatino Linotype", "Book Antiqua", serif;
  color: var(--fg);
  background-color: var(--bg);
  line-height: 1.7;
  font-size: 16px;
}

/* Content column — narrower, centered, reading-friendly */
.page {
  max-width: 750px;
  margin: 0 auto;
  padding: 2rem 1.5rem;
}

/* Sidebar */
.sidebar {
  background: var(--sidebar-bg);
  color: var(--sidebar-fg);
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  font-size: 14px;
}
.sidebar .chapter-item a {
  color: var(--sidebar-fg);
  padding: 0.3em 0.8em;
  border-radius: 4px;
  transition: background 0.15s, color 0.15s;
}
.sidebar .chapter-item a:hover {
  background: var(--sidebar-active-bg);
  color: var(--sidebar-active);
}
.sidebar .chapter-item a.active {
  background: var(--sidebar-active-bg);
  color: var(--sidebar-active);
  font-weight: 600;
}

/* Headings */
h1, h2, h3, h4, h5, h6 {
  font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
  color: var(--heading-color);
  font-weight: 600;
  line-height: 1.3;
  margin-top: 2rem;
  margin-bottom: 0.8rem;
}
h1 {
  font-size: 2rem;
  border-bottom: 2px solid var(--accent-light);
  padding-bottom: 0.4rem;
}
h2 {
  font-size: 1.5rem;
  border-bottom: 1px solid var(--accent-light);
  padding-bottom: 0.3rem;
}
h3 { font-size: 1.2rem; }
h4 { font-size: 1.1rem; }

/* Links */
a {
  color: var(--link-color);
  text-decoration: none;
  transition: color 0.15s;
}
a:hover {
  color: var(--link-hover);
  text-decoration: underline;
}

/* Code blocks */
pre, code {
  font-family: "Fira Code", "Cascadia Code", "JetBrains Mono", "Source Code Pro", monospace;
  font-size: 0.9em;
}
code {
  background: var(--code-bg);
  color: var(--code-fg);
  padding: 0.15em 0.4em;
  border-radius: 3px;
}
pre {
  background: var(--code-bg);
  border: 1px solid var(--table-border);
  border-radius: 6px;
  padding: 1em;
  overflow-x: auto;
}
pre code {
  background: transparent;
  padding: 0;
}

/* Blockquotes */
blockquote {
  background: var(--quote-bg);
  border-left: 4px solid var(--quote-border);
  margin: 1.2em 0;
  padding: 0.8em 1.2em;
  border-radius: 0 6px 6px 0;
  font-style: italic;
}

/* Lists */
ul, ol {
  padding-left: 1.5em;
}
li {
  margin-bottom: 0.3em;
}

/* Tables */
table {
  width: 100%;
  border-collapse: collapse;
  margin: 1.2em 0;
  font-size: 0.95em;
}
th, td {
  border: 1px solid var(--table-border);
  padding: 0.5em 0.8em;
  text-align: left;
}
th {
  background: var(--code-bg);
  font-weight: 600;
}
tbody tr:nth-child(even) {
  background: var(--table-alt-bg);
}

/* Images */
img {
  max-width: 100%;
  height: auto;
  display: block;
  margin: 1.5em auto;
  border-radius: 4px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
}

/* Horizontal rules */
hr {
  border: none;
  border-top: 1px solid var(--table-border);
  margin: 2em 0;
}

/* Navigation arrows (prev/next) */
.nav-chapters {
  color: var(--accent);
  font-size: 1.5em;
}

/* Search */
#searchbar {
  border: 1px solid var(--table-border);
  border-radius: 4px;
  padding: 0.4em 0.6em;
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .page {
    padding: 1rem;
  }
  h1 { font-size: 1.6rem; }
  h2 { font-size: 1.3rem; }
}
```

- [ ] **Commit**

```bash
git add LearningOfAnyKind/theme/css/general.css
git commit -m "feat: add custom CSS theme for book-like reading experience"
```

---

### Task 6: Rebuild with Custom Theme and Verify

**Files:** (none — build step)

- [ ] **Rebuild mdBook**

```bash
cd /home/atrovan/Workspace/PersonalGitHub/LearningOfAnyKind
mdbook build
```

Expected: No errors. The output in `book/` should now use the custom theme.

- [ ] **Verify custom CSS is included**

```bash
grep -c "general" book/searcher.js 2>/dev/null; grep "general.css" book/*.html | head -3
```

Expected: Custom CSS is referenced in generated HTML.

- [ ] **Commit updated build**

```bash
git add book/
git commit -m "chore: rebuild mdBook with custom theme"
```

---

### Task 7: Add GitHub Pages Deploy Workflow

**Files:**
- Create: `LearningOfAnyKind/.github/workflows/deploy.yml`

- [ ] **Create `.github/workflows/deploy.yml`**

Write to `LearningOfAnyKind/.github/workflows/deploy.yml`:

```yaml
name: Deploy mdBook to GitHub Pages

on:
  push:
    branches: [main]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: pages
  cancel-in-progress: false

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Install mdBook
        run: |
          curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y
          source "$HOME/.cargo/env"
          cargo install mdbook
      - name: Build mdBook
        run: |
          source "$HOME/.cargo/env"
          mdbook build
      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./book
  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

- [ ] **Commit**

```bash
git add LearningOfAnyKind/.github/workflows/deploy.yml
git commit -m "ci: add GitHub Pages deploy workflow for mdBook"
```

---

### Task 8: Add README Badge and Update Root README

**Files:**
- Modify: `LearningOfAnyKind/README.md`

- [ ] **Update README.md** to add a book badge and link to the hosted book

Edit `LearningOfAnyKind/README.md` — add a mdBook badge after the title:

```markdown
# LearningOfAnyKind
[![mdBook](https://img.shields.io/badge/📖-Online_Book-c0392b?style=flat-square)](https://atrovan.github.io/LearningOfAnyKind/)
Personal notes, book summaries, and random thoughts. Written in Markdown.  
```

- [ ] **Commit**

```bash
git add LearningOfAnyKind/README.md
git commit -m "docs: add book badge and link to README"
```
