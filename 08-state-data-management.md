# Phase 8: State & Data Management 💾

> **Objective:** Verify the application's state management architecture, data flow,
> and client-side storage. Web apps uniquely juggle URL state, component state,
> global stores, localStorage, cookies, and server cache.

---

## 📋 STATE CHECKS

### CHECK D1: State Architecture
```
WHAT TO CHECK:
  ❑ Is there a clear state management pattern? (Redux, Zustand, Pinia, Vuex, Signals, Context)
  ❑ Is state properly scoped? (local vs shared vs global vs server)
  ❑ Is server state separated from UI state? (React Query/SWR for server state)
  ❑ Are state updates reactive? (UI updates automatically)
  ❑ Is state serializable? (for SSR, persistence, debugging)
  ❑ Are derived values computed, not stored? (selectors, computed)

COMMON BUGS:
  🐛 Everything in global store including form input values
  🐛 Server data duplicated in local state → out of sync
  🐛 State mutation instead of immutable update → no re-render
  🐛 Derived value stored separately → gets out of sync with source
```

### CHECK D2: URL State & Deep Linking
```
WHAT TO CHECK:
  ❑ Is filter/search/pagination state in the URL? (shareable links)
  ❑ Does the back button undo filter changes?
  ❑ Are URL parameters validated? (type checking, sanitization)
  ❑ Is URL state synced with component state?
  ❑ Are deep links supported? (/products?category=shoes&sort=price)

COMMON BUGS:
  🐛 Filter state not in URL → can't share search results
  🐛 Back button doesn't undo filter → unexpected behavior
  🐛 URL parameter injection not sanitized
  🐛 Page loses all state on refresh (nothing in URL or storage)
```

### CHECK D3: Client-Side Storage
```
WHAT TO CHECK:
  ❑ Is localStorage used appropriately? (not for sensitive data)
  ❑ Are storage operations wrapped in try/catch? (quota exceeded)
  ❑ Is sessionStorage used for session-specific data?
  ❑ Is IndexedDB used for large datasets? (not localStorage)
  ❑ Is storage cleaned up? (old data removed)
  ❑ Is the user warned when storage is full?

COMMON BUGS:
  🐛 Auth token in localStorage → XSS can steal it
  🐛 localStorage.setItem without try/catch → crashes in private mode Safari
  🐛 5MB+ data stored in localStorage → quota exceeded, app breaks
  🐛 Old cache never cleared → grows indefinitely
```

### CHECK D4: Form State Management
```
WHAT TO CHECK:
  ❑ Is form state managed properly? (controlled components, React Hook Form, Formik)
  ❑ Is dirty tracking implemented? (warn before leaving unsaved form)
  ❑ Is form data preserved on navigation? (back button doesn't clear form)
  ❑ Are multi-step forms state preserved across steps?
  ❑ Is form reset handled after submission?

COMMON BUGS:
  🐛 No "unsaved changes" warning when navigating away
  🐛 Form cleared on browser back → user loses filled data
  🐛 Submit clears form before server confirms success → data lost on error
  🐛 Each keystroke triggers re-render of entire form (no debounce)
```

### CHECK D5: Cross-Tab State
```
WHAT TO CHECK:
  ❑ Is logout reflected across all tabs? (BroadcastChannel or storage event)
  ❑ Is data consistent across tabs? (edit in tab A, view in tab B)
  ❑ Are concurrent edits handled? (conflict resolution)
  ❑ Is single-tab mode enforced if needed?

COMMON BUGS:
  🐛 Logout in one tab → other tabs still functional with stale session
  🐛 Two tabs editing same record → last save wins, no warning
```

---

## 🚦 PHASE 8 GATE — MANDATORY CHECKLIST

```
PHASE 8 GATE CHECKLIST:
  □ [D1] State architecture reviewed
  □ [D2] URL state and deep linking verified
  □ [D3] Client-side storage checked
  □ [D4] Form state management assessed
  □ [D5] Cross-tab state checked
  □ Minimum 8 code citations provided
  □ Files examined list produced
```
