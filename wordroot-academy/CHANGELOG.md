# Changelog

All notable changes to **WordRoot Academy** are documented here.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.0.0/).
Versioning follows [Semantic Versioning](https://semver.org/): `MAJOR.MINOR.PATCH`

| Type | When to use |
|------|-------------|
| MAJOR | Breaking changes, full redesigns, incompatible data formats |
| MINOR | New features, new screens, new capabilities (backwards-compatible) |
| PATCH | Bug fixes, copy changes, minor UI tweaks |

---

## [Unreleased]
> Changes staged but not yet released

---

## [1.0.0] — 2025-01-01

### 🎉 Initial Release

**Student App**
- Added: Registration and login system with email + password
- Added: Role selector (Student / Parent) on auth screen
- Added: 30-minute countdown session timer with pause/resume
- Added: Language family filter — All / Latin / Greek / Anglo-Saxon
- Added: 4-step learning flow per root word:
  - Step 1 — Root Explorer: visual word tree, memory hook, click-to-expand word details with IPA pronunciation
  - Step 2 — Word Builder: prefix/suffix combination cards + common affix reference panel
  - Step 3 — In Context: literary-quality sentences + real author quotes
  - Step 4 — Revision Quiz: multiple-choice meaning test with instant feedback
- Added: XP reward system (+5 explore, +20 quiz correct, +50 root complete)
- Added: Session history panel showing all roots studied
- Added: Student stats panel with monthly goal progress bar
- Added: Session complete screen with full performance summary
- Added: Graceful offline fallback root (PORT) when API unavailable

**Parent Dashboard**
- Added: Silent background tracking — saves session data without student awareness
- Added: Parent login with linked student email field
- Added: KPI grid: total roots, words, sessions, time, quiz accuracy, XP, last active, unique roots
- Added: Monthly goal bar (target: 1,000 roots/month)
- Added: Per-session bar chart (last 7 sessions)
- Added: Session history table (last 10 sessions) with date, roots, words, duration, quiz score
- Added: Language family coverage bars (Latin / Greek / Anglo-Saxon)
- Added: All words explored grid with root, meaning, date
- Added: All unique roots completed list

**Technical**
- Added: localStorage-based persistence (no backend required)
- Added: All data namespaced under `wra:` prefix to avoid collisions
- Added: `APP_VERSION` and `APP_BUILD` constants in JS
- Added: Version badge displayed in bottom-right corner
- Added: Anthropic Claude claude-sonnet-4-20250514 API integration for dynamic root generation
- Added: Prompt engineering for etymology-rich, age-appropriate content
- Added: Mobile-responsive layout (breakpoint at 640px)

---

## Version Roadmap

### [1.1.0] — Planned
- [ ] Password reset flow
- [ ] Weekly email summary to parent (via EmailJS or similar free service)
- [ ] Streak tracking across sessions (persistent day counter)
- [ ] Sound effects and animations for quiz correct/wrong
- [ ] Print/export session report as PDF

### [1.2.0] — Planned
- [ ] Cross-device sync via Firebase Firestore (free tier)
- [ ] Multiple student profiles under one parent account
- [ ] Word bookmarking — student can save favourite words
- [ ] Spaced repetition review — revisit weak words automatically

### [2.0.0] — Planned
- [ ] Full PWA (Progressive Web App) — installable on phone
- [ ] Offline mode with cached root database (100+ pre-loaded roots)
- [ ] Audio pronunciation playback
- [ ] Parent push notifications for missed sessions
