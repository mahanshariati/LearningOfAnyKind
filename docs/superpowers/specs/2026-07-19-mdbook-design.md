# mdBook Visual Overhaul for Book Notes

Date: 2026-07-19

## Overview

Transform the `books/` directory of `LearningOfAnyKind` from raw markdown files into a polished, browsable online book using [mdBook](https://rust-lang.github.io/mdBook/). No existing `.md` file content is modified.

## Project Structure

```
LearningOfAnyKind/
├── book.toml               # mdBook configuration
├── books/                  # mdBook source directory (existing content lives here)
│   ├── SUMMARY.md          # Table of contents (NEW)
│   ├── FundamentalOfSoftwareEngineering.md
│   ├── HandsOnSofwareEngineeringWithGolang.md
│   ├── LearningGo_AnIdiomaticApproachToRealWorldGoProgramming.md
│   ├── LPIC-1.MD
│   ├── PythonProgrammingAnIntroductionToComputerScience.md
│   ├── UnitTesting.md
│   └── images/
├── theme/                  # Custom theme overrides (NEW)
│   └── css/
│       └── general.css     # Custom stylesheet (NEW)
└── .github/
    └── workflows/
        └── deploy.yml      # GitHub Pages auto-deploy (NEW, optional)
```

## Configuration (`book.toml`)

- `title`: "Learning of Any Kind"
- `src`: "books" (source directory)
- `theme`: "theme" (custom theme directory)
- `site-url`: GitHub Pages URL
- Output to `book/html/`

## Navigation (`SUMMARY.md`)

Each existing markdown file becomes a chapter. Clean display titles derived from content (not raw filenames). The project root `README.md` cross-references books as a subdirectory, so it stays as the repo README but isn't a book chapter.

## Visual Theme (CSS)

The `general.css` customizes:
- **Typography**: Serif font for body (reading comfort), sans-serif for headings, good font sizes and line-height
- **Color scheme**: Warm, book-like palette — cream/off-white background (#faf8f5), dark charcoal text (#2d2d2d), muted accent (#c0392b or similar warm accent)
- **Layout**: Centered content column (max-width ~750px), generous padding
- **Headings**: Distinct visual hierarchy with subtle underlines or color shifts
- **Code blocks**: Soft background (#f5f0eb), subtle border
- **Links**: Underline on hover, accent color
- **Tables**: Striped rows, clean borders
- **Images**: Max-width constrained, centered, subtle shadow
- **Navigation sidebar**: Clean, hierarchical, current-page highlight

## GitHub Pages Deployment

A GitHub Action workflow auto-builds and deploys the mdBook on push to main. The site is available at `https://<user>.github.io/LearningOfAnyKind/`.

## Constraints

- No existing `.md` content is altered
- No file deletion or renaming
- The project remains valid as plain markdown (mdBook is additive)
