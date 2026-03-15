# Storage Schema — WordRoot Academy

All data is stored in `localStorage` with the prefix `wra:` to avoid collisions with other apps.

---

## Key Naming Convention

```
wra:{type}:{identifier}:{timestamp}
```

---

## Schema Reference

### User Account
**Key:** `wra:user:{email}`

```json
{
  "name": "Priya Sharma",
  "email": "priya@example.com",
  "role": "student",
  "createdAt": 1704067200000,
  "linkedStudent": null,
  "appVersion": "1.0.0"
}
```

For a parent:
```json
{
  "name": "Jai Sharma",
  "email": "jai@example.com",
  "role": "parent",
  "createdAt": 1704067200000,
  "linkedStudent": "priya@example.com",
  "appVersion": "1.0.0"
}
```

---

### Password
**Key:** `wra:pass:{email}`

```
"cHJpeWExMjM="   ← Base64-encoded password string
```

---

### Student Index
**Key:** `wra:index:{email}`

```json
{
  "studentName": "Priya Sharma",
  "sessions": [1704067200000, 1704153600000],
  "lastActive": 1704153600000
}
```

---

### Session Record
**Key:** `wra:session:{email}:{startTimestamp}`

```json
{
  "studentEmail": "priya@example.com",
  "studentName": "Priya Sharma",
  "appVersion": "1.0.0",
  "startTime": 1704067200000,
  "lastUpdated": 1704069000000,
  "durationMin": 28,
  "rootsCompleted": 4,
  "rootsSkipped": 1,
  "rootsData": [
    {
      "root": "PORT",
      "meaning": "carry",
      "origin": "Latin",
      "completedAt": 1704067500000,
      "skipped": false,
      "words": ["TRANSPORT", "IMPORT", "EXPORT", "PORTFOLIO", "DEPORTMENT"]
    }
  ],
  "wordsExplored": 18,
  "wordsData": [
    {
      "word": "TRANSPORT",
      "root": "PORT",
      "meaning": "to carry across from one place to another",
      "complexity": "beginner",
      "learnedAt": 1704067320000
    }
  ],
  "quizCorrect": 3,
  "quizTotal": 4,
  "xpEarned": 245
}
```

---

## Storage Size Estimates

| Record Type | Est. Size | Frequency |
|-------------|-----------|-----------|
| User account | ~200 bytes | Once per user |
| Password | ~20 bytes | Once per user |
| Student index | ~100 bytes + 8 bytes/session | Updated each session |
| Session record | ~2–5 KB | Once per 30-min session |

At 30 sessions/month × 5 KB = **~150 KB/month**. localStorage limit is typically 5–10 MB, so this supports **years of usage** without hitting limits.

---

## Clearing Data

To reset all app data from browser DevTools console:
```javascript
// Clear all WordRoot Academy data
Object.keys(localStorage)
  .filter(k => k.startsWith('wra:'))
  .forEach(k => localStorage.removeItem(k));
console.log('All WordRoot Academy data cleared');
```

To clear only sessions for one student:
```javascript
const email = 'priya@example.com';
Object.keys(localStorage)
  .filter(k => k.startsWith(`wra:session:${email}`))
  .forEach(k => localStorage.removeItem(k));
```
