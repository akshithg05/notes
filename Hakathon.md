

---

## Overview: A11y Pre-Commit Accessibility Checker

### What problem does it solve?

Accessibility bugs are cheap to fix at **write time** and expensive to fix after release. This tool catches them **before they ever reach the repo** — at the moment a developer runs `git commit`.

---

### Architecture (6 modules)

```
scripts/a11y/
├── index.js        ← Orchestrator: decides staged vs full scan, runs the pipeline
├── fileFilter.js   ← Git integration: finds staged files or walks src/ on disk
├── jsxToHtml.js    ← JSX transformer: converts React source to real HTML
├── runner.js       ← axe-core engine: spins up jsdom, injects axe, runs checks
├── scorer.js       ← Scoring: starts at 100, deducts per severity
└── reporter.js     ← Output: colorized CLI + structured JSON report
```

---

### How accessibility detection works (the pipeline)

```
git commit
    │
    ▼
[fileFilter.js]  ──  git diff --cached --name-only
    │                Filters: .js .jsx .ts .tsx .html
    │                Reads staged content (not working dir)
    ▼
[jsxToHtml.js]   ──  JSX → real HTML
    │                • Extracts return() and => () blocks
    │                • Converts PascalCase components → <div>
    │                • Converts JSX attrs: className→class, htmlFor→for
    │                • Handles nested JSX expressions
    ▼
[runner.js]      ──  jsdom + axe-core
    │                • Creates a real DOM from the HTML
    │                • Injects axe-core into the DOM context
    │                • Runs axe.run() - same engine used in browser devtools
    │                • Maps violations back to source line numbers
    ▼
[scorer.js]      ──  Score = 100 − Σ(penalties per issue)
    │                critical: -10 | serious: -7 | moderate: -4 | minor: -1
    ▼
[reporter.js]    ──  CLI output (colorized) + a11y-report.json
```

---

### What axe-core checks (WCAG 2.1 rules)

| Category | Example rules caught |
|---|---|
| **Images** | Missing `alt` on `<img>`, SVGs without labels |
| **Buttons/Links** | Empty `<button>`, `<a>` with no text |
| **Forms** | `<input>` without `<label>`, `<select>` without name |
| **ARIA** | Invalid `aria-*` attributes, `aria-hidden` on focusable elements |
| **Structure** | Heading order skipped (h1→h3), content outside landmarks |
| **HTML** | Missing `lang` on `<html>`, missing `<title>` |

Color contrast is **disabled** (jsdom can't compute CSS) — that's caught by browser devtools separately.

---

### Scoring system

```
Start:  100
─────────────────────────────
critical  issue  →  -10 each   (e.g. missing alt text)
serious   issue  →   -7 each   (e.g. empty link)
moderate  issue  →   -4 each   (e.g. missing landmark)
minor     issue  →   -1 each
─────────────────────────────
Floor:      0    (never goes negative)
Threshold: 80    (below this = commit blocked)
```

---

### How to use

**Normal daily use — automatic on every commit:**
```sh
git add src/components/MyComponent.jsx
git commit -m "feat: add button"
# ↑ hook runs automatically, blocks if score < 80
```

**Emergency bypass:**
```sh
git commit --no-verify -m "hotfix: urgent"
```

**Manual check on staged files:**
```sh
yarn a11y:check
```

**Report on a single component folder:**
```sh
node scripts/a11y/index.js --all src/components/SustainabilityAnalysisPageV2
```

**Full application report:**
```sh
yarn a11y:report          # scans all 1143 files in src/
# or with more memory:
node --max-old-space-size=4096 scripts/a11y/index.js --all
```

---

### Output

**CLI:**
```
Accessibility Score: 41/100

Issues:

  Button.jsx
    • [critical] Buttons must have discernible text (button-name) — line 4
    • [critical] Images must have alternative text (image-alt) — line 3
    • [serious]  Links must have discernible text (link-name) — line 6

Report saved to: ./a11y-report.json

✗ Score 41/100 is below threshold (80). Commit blocked.
  Use "git commit --no-verify" to bypass.
```

**a11y-report.json** (AI-consumable):
```json
{
  "score": 41,
  "timestamp": "2026-04-13T04:11:13.300Z",
  "filesChecked": 1,
  "totalIssues": 6,
  "issues": [
    {
      "file": "Button.jsx",
      "line": 4,
      "rule": "button-name",
      "severity": "critical",
      "description": "Buttons must have discernible text",
      "suggestion": "Ensure the button has visible text, aria-label, or aria-labelledby."
    }
  ]
}
```

---

### Key design decisions for demo

| Decision | Why |
|---|---|
| **Husky v4** (already in repo) | Zero new tooling to install |
| **axe-core** | Industry standard — same engine as Chrome DevTools, Lighthouse, and Deque |
| **jsdom** (already in repo via Jest) | No headless browser needed — fast and lightweight |
| **JSX→HTML transform** | axe-core needs a real DOM; this bridges the gap without a build step |
| **Staged content only** (pre-commit) | Never slows down by reading unchanged files |
| **Exit 0 on tool failure** | Tool errors never block developer commits |