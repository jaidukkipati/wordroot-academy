# WordRoot Academy 📚

> AI-powered etymology workbook — master Latin, Greek & Anglo-Saxon root words through a structured 4-step learning system, with a silent parent monitoring dashboard.

![Version](https://img.shields.io/badge/version-1.0.0-brightgreen)
![License](https://img.shields.io/badge/license-MIT-blue)
![Deploy](https://img.shields.io/badge/deploy-GitHub%20Pages-orange)
![Storage](https://img.shields.io/badge/storage-localStorage-yellow)

---

## ✨ What Is This?

WordRoot Academy is a single-file web application designed for a 17-year-old student to learn vocabulary through etymology. The goal is **1,000 root words per month** in **30-minute daily sessions**.

Every root word goes through 4 structured learning steps:

| Step | Name | What Happens |
|------|------|--------------|
| 1 | Root Explorer | Learn the root, its origin, memory hook, and explore 6–8 branching words |
| 2 | Word Builder | See how prefixes and suffixes combine with the root to create new words |
| 3 | In Context | Read the words in literary-quality sentences and real author quotes |
| 4 | Revision Quiz | Multiple-choice test with instant feedback and XP rewards |

A **parent dashboard** runs silently in the background, recording every session, every word explored, and every quiz result — invisible to the student.

---

## 🚀 Live Demo

Deploy to GitHub Pages (see [Deployment](#-deployment) below).

---

## 📁 Project Structure

```
wordroot-academy/
│
├── index.html              # ← The entire application (single file)
│
├── CHANGELOG.md            # ← Version history and roadmap
├── README.md               # ← This file
├── LICENSE                 # ← MIT License
│
├── .github/
│   ├── workflows/
│   │   └── deploy.yml      # ← GitHub Actions: auto-deploy to Pages on push
│   └── ISSUE_TEMPLATE/
│       ├── bug_report.md
│       └── feature_request.md
│
├── releases/
│   ├── v1.0.0.html         # ← Archived snapshot of each release
│   └── RELEASE_NOTES.md    # ← Human-readable release notes per version
│
└── docs/
    ├── ARCHITECTURE.md     # ← Technical architecture decisions
    ├── STORAGE_SCHEMA.md   # ← localStorage key/value schema
    └── VERSIONING.md       # ← How we version this project
```

---

## 🛠 Tech Stack

| Layer | Technology | Why |
|-------|-----------|-----|
| Frontend | Vanilla HTML/CSS/JS | Zero dependencies, one file, instant load |
| Fonts | Google Fonts (Fraunces, DM Sans, Fira Mono) | Beautiful typography, CDN-hosted |
| AI Content | Anthropic Claude claude-sonnet-4-20250514 | Infinite dynamic root generation |
| Storage | `localStorage` | No backend needed, works on any host |
| Hosting | GitHub Pages | Free, permanent URL, version-controlled |

---

## 🔐 Authentication

The app has its own lightweight auth system stored in `localStorage`:

- **Student** registers with name, email, password → gets the learning app
- **Parent** registers with name, email, password + optional student email → gets the monitoring dashboard
- Passwords are stored as Base64-encoded strings (suitable for personal/family use; not production-grade cryptography)
- All data is stored in the **same browser** on the **same device**

> **Note:** For cross-device access (e.g. student on laptop, parent on phone), upgrade to Firebase storage. See `docs/ARCHITECTURE.md`.

---

## 📊 Parent Dashboard — What It Tracks (Silently)

Every time the student completes or skips a root, a session snapshot is saved automatically. The parent sees:

- Total roots completed, words explored, sessions count, time studied
- Quiz accuracy across all sessions
- Monthly progress toward the 1,000 roots/month goal
- Per-session bar chart (roots learned per session)
- Full session history table with date, time, duration, quiz score
- Language family breakdown (Latin / Greek / Anglo-Saxon)
- Every single word the student clicked on, with definition and date
- Every root completed, with origin and meaning

**The student sees none of this.** There is no visible tracking indicator anywhere in the student view.

---

## 🌐 Deployment

### Option 1 — GitHub Pages (Recommended)

1. Fork or clone this repository
2. Go to your repo → **Settings → Pages**
3. Source: **Deploy from branch** → `main` → `/ (root)`
4. Save — your app is live at `https://YOUR-USERNAME.github.io/wordroot-academy`

GitHub Actions (`.github/workflows/deploy.yml`) will auto-deploy every time you push to `main`.

### Option 2 — Netlify Drop

1. Go to [netlify.com/drop](https://netlify.com/drop)
2. Drag `index.html` onto the page
3. Get your URL instantly

### Option 3 — Vercel

1. Sign up at [vercel.com](https://vercel.com)
2. Import this GitHub repo
3. Deploy — done

---

## 🔄 Version Management

This project uses **Semantic Versioning** (`MAJOR.MINOR.PATCH`).

### When you make a change:

1. **Edit `index.html`** — make your changes
2. **Update version constants** in `index.html`:
   ```javascript
   const APP_VERSION = '1.1.0';  // ← bump this
   const APP_BUILD   = '2025-02-01';  // ← update date
   ```
3. **Update `CHANGELOG.md`** — document what changed under a new `[1.1.0]` heading
4. **Archive a release copy**:
   ```bash
   cp index.html releases/v1.1.0.html
   ```
5. **Commit with a clear message**:
   ```bash
   git add .
   git commit -m "v1.1.0 — Add password reset and streak tracking"
   git push
   ```
6. **Tag the release** on GitHub:
   ```bash
   git tag -a v1.1.0 -m "v1.1.0 — Add password reset and streak tracking"
   git push origin v1.1.0
   ```

### Commit message convention:

```
v1.1.0 — Short description of what changed

- Added: new feature
- Fixed: bug description
- Changed: what was modified
- Removed: what was deleted
```

---

## 🧪 Testing Checklist

Before pushing any change, verify:

**Auth**
- [ ] Student registration works
- [ ] Parent registration works with linked student email
- [ ] Login works for both roles
- [ ] Wrong password shows error
- [ ] Logout clears state

**Student App**
- [ ] Timer starts, pauses, resumes correctly
- [ ] Language family filter changes root origin
- [ ] All 4 steps render without errors
- [ ] Word detail opens on click
- [ ] Quiz accepts answer and shows feedback
- [ ] Root complete saves to localStorage
- [ ] Skip root saves to localStorage
- [ ] Session end screen appears at 0:00
- [ ] New session resets state correctly

**Parent Dashboard**
- [ ] Parent sees linked student after student has completed a root
- [ ] All KPI values are correct
- [ ] Session history table populates
- [ ] Word list shows explored words
- [ ] Monthly bar reflects correct count

**Offline / Fallback**
- [ ] Fallback root loads when API fails
- [ ] App does not crash on network error

---

## 📝 License

MIT License — free to use, modify, and distribute.

---

## 👨‍👩‍👧 Made For

A parent and their daughter — to make vocabulary learning structured, measurable, and genuinely enjoyable.
