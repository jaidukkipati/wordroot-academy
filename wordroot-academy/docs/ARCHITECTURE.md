# Architecture — WordRoot Academy

## Overview

WordRoot Academy is a **single-file web application** — everything lives in `index.html`. This is a deliberate architectural choice for simplicity of deployment and maintenance.

```
Browser
  │
  ├── index.html (HTML + CSS + JS)
  │     ├── Auth Layer (localStorage)
  │     ├── Student App (3 panels)
  │     │     ├── Learn (4-step flow)
  │     │     ├── History
  │     │     └── Stats
  │     └── Parent Dashboard
  │
  ├── Anthropic API (claude-sonnet-4-20250514)
  │     └── Dynamic root word generation
  │
  └── localStorage
        ├── User accounts
        ├── Session records
        └── Student indexes
```

---

## Key Design Decisions

### 1. Single HTML File
**Why:** Zero build step, zero dependencies, deployable anywhere, easy to version-control and diff.

**Trade-off:** All CSS and JS are inline. For larger apps this would be split into separate files.

### 2. localStorage (not a database)
**Why:** No backend needed, instant setup, free forever, works offline after first load.

**Trade-off:** Data is per-device per-browser. If the student uses a different browser or device, data won't carry over.

**Upgrade path:** Replace the 3 storage functions (`storeGet`, `storeSet`, `storeList`) with Firebase Firestore calls. The rest of the app doesn't need to change.

### 3. Anthropic API called from the browser
**Why:** Simplest integration — no server needed.

**Trade-off:** The API key (if one were used) would be exposed in the browser. In this app, the API key is injected by the Claude.ai artifact environment automatically — it is NOT hardcoded in the source file. For a public deployment, you should proxy through a lightweight serverless function (Netlify Functions, Vercel Edge Functions).

### 4. No framework (vanilla JS)
**Why:** Fastest load, no dependencies to update, no build pipeline needed.

**Trade-off:** State management is manual. For larger scale, React or Svelte would be cleaner.

---

## How Silent Tracking Works

The student never sees any tracking UI. The mechanism:

1. `completeRoot()` and `skipRoot()` both call `saveSession()`
2. `saveSession()` writes a `session:email:timestamp` record to localStorage
3. The parent dashboard reads all keys matching `session:{linkedStudentEmail}:*`
4. No network request is made — it's all local storage reads

This means:
- No notification to the student
- No visible badge or counter
- Data is saved even if the timer is still running (incremental saves)

---

## Upgrade: Cross-Device Monitoring with Firebase

To allow the parent to monitor from a different device:

1. Create a free Firebase project at [firebase.google.com](https://firebase.google.com)
2. Enable Firestore database
3. Replace the 3 storage functions in `index.html`:

```javascript
// Replace storeGet / storeSet / storeList with:
import { initializeApp } from 'https://www.gstatic.com/firebasejs/10.x/firebase-app.js';
import { getFirestore, doc, setDoc, getDoc, collection, getDocs } from 'https://www.gstatic.com/firebasejs/10.x/firebase-firestore.js';

const app = initializeApp({ /* your firebase config */ });
const db = getFirestore(app);

async function storeGet(key) {
  const snap = await getDoc(doc(db, 'wordroot', key));
  return snap.exists() ? snap.data().value : null;
}
async function storeSet(key, val) {
  await setDoc(doc(db, 'wordroot', key), { value: val });
}
async function storeList(prefix) {
  // Query Firestore collection for keys starting with prefix
  // Implementation depends on your data model
}
```

This is a v1.2.0 planned upgrade — see CHANGELOG.md.

---

## Security Notes

- Passwords are Base64-encoded (not hashed). This is appropriate for a personal family app, not for a public product.
- For a production app, use bcrypt (server-side) or a proper auth service like Firebase Auth or Clerk.
- The Anthropic API key is never stored in the source code. It is provided by the deployment environment.
