# Phase 7: API & Network Resilience 🌐

> **Objective:** Test all network-dependent functionality for robustness, error handling,
> and graceful degradation. Web apps live and die by their API calls.

---

## 📋 NETWORK CHECKS

### CHECK N1: API Communication Layer
```
WHAT TO CHECK:
  ❑ Is there a centralized HTTP client? (Axios instance, fetch wrapper)
  ❑ Are API base URLs configurable? (env vars, not hardcoded)
  ❑ Is authentication handled centrally? (interceptors for token injection)
  ❑ Are request/response types defined? (TypeScript interfaces, Zod)
  ❑ Is request deduplication implemented? (React Query, SWR)
  ❑ Are API errors typed and handled consistently?

COMMON BUGS:
  🐛 fetch() scattered across 50 files with different error handling
  🐛 Base URL hardcoded — can't switch between dev/staging/prod
  🐛 Same API called 5 times on page load (no dedup)
  🐛 Token refresh race condition → multiple refresh requests
```

### CHECK N2: Error Handling & Retry
```
WHAT TO CHECK:
  ❑ Are HTTP errors handled by status code? (401→logout, 403→forbidden, 404→not found, 500→generic)
  ❑ Is retry logic implemented with exponential backoff?
  ❑ Are retries limited? (max 3 attempts)
  ❑ Are non-retryable errors identified? (400, 401, 403, 422)
  ❑ Are timeouts configured for all requests?
  ❑ Is the user notified of persistent failures?

COMMON BUGS:
  🐛 All errors show "Something went wrong" (no differentiation)
  🐛 Infinite retry on 400 Bad Request
  🐛 No timeout → request hangs forever on slow network
  🐛 401 doesn't redirect to login → user sees broken page
```

### CHECK N3: Loading & Empty States
```
WHAT TO CHECK:
  ❑ Is there a loading state for every async operation?
  ❑ Are skeleton screens used instead of spinners?
  ❑ Is the empty state informative? ("No results" with action suggestion)
  ❑ Is the error state actionable? ("Retry" button)
  ❑ Is the loading state accessible? (aria-busy, aria-live)

COMMON BUGS:
  🐛 No loading indicator → user thinks page is broken
  🐛 Empty state shows blank page instead of helpful message
  🐛 Error state with no retry option → user must refresh manually
```

### CHECK N4: Offline & Slow Network
```
WHAT TO CHECK:
  ❑ Does the app show an offline indicator?
  ❑ Are critical features available offline? (if PWA)
  ❑ Does the app recover gracefully when connection returns?
  ❑ Are form submissions queued when offline?
  ❑ Does the app handle slow 3G-like networks?

COMMON BUGS:
  🐛 App crashes immediately when offline
  🐛 Form submission lost when submitted offline
  🐛 No offline indicator — user thinks actions are saved
  🐛 App hangs on slow network — no timeout
```

### CHECK N5: Data Fetching Patterns
```
WHAT TO CHECK:
  ❑ Is data fetched at the right level? (page vs component)
  ❑ Are waterfalls avoided? (parallel fetching)
  ❑ Is stale data shown while revalidating? (SWR pattern)
  ❑ Is pagination implemented correctly? (cursor vs offset)
  ❑ Is infinite scroll using intersection observer?
  ❑ Are prefetch/preload hints used for likely navigation?
```

---

## 🚦 PHASE 7 GATE — MANDATORY CHECKLIST

```
PHASE 7 GATE CHECKLIST:
  □ [N1] API communication layer reviewed
  □ [N2] Error handling and retry logic verified
  □ [N3] Loading and empty states checked
  □ [N4] Offline and slow network behavior tested
  □ [N5] Data fetching patterns assessed
  □ Minimum 10 code citations provided
  □ Files examined list produced
```
