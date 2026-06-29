# Docs Site on GitHub Pages — Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Publish the existing markdown files as a searchable docs website on GitHub Pages using Docsify (no build step).

**Architecture:** Docsify loads `index.html` from the repo root, reads `_sidebar.md` for navigation, and renders every `.md` file on the fly in the browser. GitHub Pages serves the static files directly — no CI, no Jekyll, no build pipeline.

**Tech Stack:** Docsify 4 (CDN), GitHub Pages (root branch `main`)

## Global Constraints

- No npm install, no build step — everything served from CDN via `index.html`
- All existing `.md` files stay in the repo root — do not move or rename them
- Thai-language content must render correctly (UTF-8, `lang="th"`)
- Site must work at `https://<username>.github.io/<repo-name>/`
- `.nojekyll` file required in root to prevent GitHub Pages Jekyll processing

---

## File Structure

```
web-ai/
├── index.html          ← Docsify bootstrap (CREATE)
├── _sidebar.md         ← Navigation links (CREATE)
├── .nojekyll           ← Empty file, disables Jekyll (CREATE)
├── README.md           ← Homepage content (already exists, keep as-is)
├── 00-overview.md      ← (existing, untouched)
├── 00-core-concept.md  ← (existing, untouched)
├── 01-*.md … 20-*.md  ← (existing, untouched)
└── docs/superpowers/plans/  ← (this plan, ignored by site)
```

---

### Task 1: Scaffold Docsify files

**Files:**
- Create: `index.html`
- Create: `_sidebar.md`
- Create: `.nojekyll`

**Interfaces:**
- Produces: a working local Docsify site at `http://localhost:3000`

- [ ] **Step 1: Create `index.html`**

Create `/Users/ananchaiphahupongsub/work/web-ai/index.html` with this exact content:

```html
<!DOCTYPE html>
<html lang="th">
<head>
  <meta charset="UTF-8">
  <title>AI Project Context Kit</title>
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/docsify@4/lib/themes/vue.css">
</head>
<body>
  <div id="app"></div>
  <script>
    window.$docsify = {
      name: 'AI Project Context Kit',
      loadSidebar: true,
      subMaxLevel: 2,
      search: 'auto',
      coverpage: false,
    }
  </script>
  <script src="https://cdn.jsdelivr.net/npm/docsify@4/lib/docsify.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/docsify@4/lib/plugins/search.min.js"></script>
</body>
</html>
```

- [ ] **Step 2: Create `_sidebar.md`**

Create `/Users/ananchaiphahupongsub/work/web-ai/_sidebar.md` with this exact content:

```markdown
- [Home](README.md)
- **Getting Started**
  - [Overview](00-overview.md)
  - [Core Concept](00-core-concept.md)
- **Setup**
  - [Recommended Project Structure](01-recommended-project-structure.md)
  - [Tool-Specific Instruction Files](02-tool-specific-instruction-files.md)
  - [Minimum Setup](18-minimum-setup.md)
- **Standards**
  - [Team AI Standard](03-team-ai-standard-md.md)
  - [Architecture](04-architecture-md.md)
  - [File Ownership](05-file-ownership-md.md)
  - [Commands](06-commands-md.md)
  - [Backend Standard](07-backend-standard-md.md)
  - [Frontend Standard](08-frontend-standard-md.md)
  - [Database Standard](09-database-standard-md.md)
  - [Testing Standard](10-testing-standard-md.md)
  - [Review Standard](11-review-standard-md.md)
- **Reference**
  - [Examples](12-examples-md.md)
  - [Definition of Done](13-definition-of-done-md.md)
  - [Task Template](14-task-template-md.md)
  - [Harness Agents](15-harness-agents.md)
  - [Skills](16-skills.md)
- **Advanced**
  - [End-to-End Workflow](17-example-end-to-end-workflow.md)
  - [Anti-Patterns](19-anti-patterns.md)
  - [Final Summary](20-final-summary.md)
```

- [ ] **Step 3: Create `.nojekyll`**

Create an empty file at `/Users/ananchaiphahupongsub/work/web-ai/.nojekyll`:

```bash
touch /Users/ananchaiphahupongsub/work/web-ai/.nojekyll
```

- [ ] **Step 4: Verify locally**

Run a local server from the project root:

```bash
cd /Users/ananchaiphahupongsub/work/web-ai
python3 -m http.server 3000
```

Open `http://localhost:3000` in a browser.

Expected:
- Left sidebar shows all sections and links
- Clicking a link renders the Thai markdown content
- Search bar in top-left works
- No 404 errors in browser console

Stop server with `Ctrl+C` when done.

- [ ] **Step 5: Commit**

```bash
cd /Users/ananchaiphahupongsub/work/web-ai
git init
git add index.html _sidebar.md .nojekyll
git commit -m "feat: add Docsify scaffold for GitHub Pages"
```

---

### Task 2: Push to GitHub and enable Pages

**Files:** No new files — GitHub configuration via `gh` CLI.

**Interfaces:**
- Consumes: committed repo from Task 1
- Produces: live site at `https://<username>.github.io/<repo-name>/`

- [ ] **Step 1: Create GitHub repo**

```bash
cd /Users/ananchaiphahupongsub/work/web-ai
gh repo create web-ai --public --source=. --remote=origin --push
```

Expected output: `✓ Created repository <username>/web-ai on GitHub` and a push confirmation.

- [ ] **Step 2: Enable GitHub Pages**

```bash
gh api repos/{owner}/{repo}/pages \
  --method POST \
  -f source='{"branch":"main","path":"/"}' \
  --jq '.html_url'
```

Replace `{owner}` and `{repo}` with your GitHub username and `web-ai`.

Expected output: `https://<username>.github.io/web-ai/`

- [ ] **Step 3: Wait ~60 seconds, then verify**

```bash
sleep 60
curl -sI https://<username>.github.io/web-ai/ | head -5
```

Expected: `HTTP/2 200`

- [ ] **Step 4: Open in browser and do a smoke check**

Open `https://<username>.github.io/web-ai/` in a browser.

Verify:
- Homepage loads (README.md content visible)
- Sidebar navigation works
- At least one Thai-language page renders correctly (try clicking "Overview")
- Search returns results when you type a Thai word

---

## Self-Review

**Spec coverage:**
- Markdown files as content → Task 1 (`_sidebar.md` links all 21 files, existing files untouched)
- Docs site layout → Task 1 (Docsify vue theme + sidebar)
- GitHub Pages deployment → Task 2 (gh CLI + Pages API)
- No build step → confirmed, CDN-only approach
- Thai content → `lang="th"` + UTF-8 in `index.html`

**Placeholder scan:** None found — all steps have exact commands and expected output.

**Type consistency:** N/A — no custom code, only config files.
