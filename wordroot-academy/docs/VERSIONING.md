# Versioning Guide — WordRoot Academy

## How We Version

This project uses **Semantic Versioning**: `MAJOR.MINOR.PATCH`

```
  1  .  0  .  0
  │     │     │
  │     │     └── PATCH: bug fixes, typo corrections, minor UI tweaks
  │     └──────── MINOR: new features, new screens (backwards-compatible)
  └────────────── MAJOR: breaking changes, redesigns, incompatible data
```

---

## Step-by-Step: How to Release a New Version

### Step 1 — Make Your Changes
Edit `index.html`. Test locally by opening in a browser.

### Step 2 — Update Version in index.html
Find these two lines near the top of the `<script>` block:

```javascript
const APP_VERSION = '1.0.0';   // ← change this
const APP_BUILD   = '2025-01-01'; // ← change to today's date
```

### Step 3 — Update CHANGELOG.md
Add a new section at the top (below `[Unreleased]`):

```markdown
## [1.1.0] — 2025-02-01

### Added
- Password reset flow via email link
- Day streak tracking across sessions

### Fixed
- Quiz options sometimes showing duplicate answers

### Changed
- Session timer now shows seconds more prominently
```

### Step 4 — Archive a Release Copy
```bash
cp index.html releases/v1.1.0.html
```

### Step 5 — Commit Everything
```bash
git add index.html CHANGELOG.md releases/v1.1.0.html
git commit -m "v1.1.0 — Add password reset and streak tracking"
```

### Step 6 — Push to GitHub
```bash
git push origin main
```
GitHub Actions will automatically deploy to GitHub Pages.

### Step 7 — Tag the Release
```bash
git tag -a v1.1.0 -m "Release v1.1.0"
git push origin v1.1.0
```

Then on GitHub.com: go to **Releases → Draft a new release → Choose tag v1.1.0 → Publish**.

---

## Commit Message Convention

```
v{version} — {short description}

- Added: {new feature}
- Fixed: {bug fixed}  
- Changed: {what was modified}
- Removed: {what was deleted}
```

Examples:
```
v1.0.1 — Fix quiz options sometimes duplicating

v1.1.0 — Add password reset and weekly streak badge

v1.2.0 — Add Firebase cross-device sync

v2.0.0 — Full PWA with offline support and audio pronunciation
```

---

## What Lives in /releases

Every time a version is released, a snapshot of `index.html` is saved as `releases/v{version}.html`.

This lets you:
- See exactly what the app looked like at any version
- Roll back by copying a release file over `index.html`
- Compare two versions with a diff tool

```bash
# Roll back to v1.0.0
cp releases/v1.0.0.html index.html
git add index.html
git commit -m "revert: roll back to v1.0.0"
git push
```
