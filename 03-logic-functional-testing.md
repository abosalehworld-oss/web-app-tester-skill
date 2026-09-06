# Phase 3: Logic & Functional Testing 🧠

> **Objective:** Verify all business logic, state transitions, data validation, and
> computational functions work correctly — including edge cases that real users will hit.

---

## 📋 LOGIC CHECKS

### CHECK L1: Input Validation
```
WHAT TO CHECK:
  ❑ Are ALL user inputs validated both client-side AND server-side?
  ❑ Are boundary values handled? (min/max lengths, numeric limits)
  ❑ Are special characters handled? (unicode, emoji, RTL text, null bytes)
  ❑ Are empty/null/undefined inputs handled gracefully?
  ❑ Is type coercion safe? (string to number, date parsing)
  ❑ Are URL parameters and query strings validated?
  ❑ Is file upload type and size validated?

COMMON BUGS:
  🐛 Client-side validation only → bypassed via DevTools or curl
  🐛 Pasted text bypasses character validation (onKeyPress only)
  🐛 URL parameter /?id=undefined crashes the component
  🐛 Search query with regex special chars crashes filter
  🐛 File upload accepts .exe disguised as .jpg
```

### CHECK L2: State Machine & Workflow Logic
```
WHAT TO CHECK:
  ❑ Are there clear state definitions? (enum, constants, types)
  ❑ Are invalid state transitions prevented?
  ❑ Is the current state always visible to the user?
  ❑ Can the user undo/redo actions?
  ❑ Is state preserved on page refresh? (URL state, localStorage)
  ❑ Are multi-step forms (wizards) properly managed?

COMMON BUGS:
  🐛 Submit button enabled before form is valid
  🐛 Multi-step form loses data on browser back
  🐛 State gets stuck — no way to recover without refresh
  🐛 Refreshing page resets checkout to step 1
```

### CHECK L3: Calculation & Data Processing
```
WHAT TO CHECK:
  ❑ Are floating-point calculations handled correctly? (use Decimal/cents for money)
  ❑ Are date/time operations timezone-aware?
  ❑ Are sorting algorithms stable and correct?
  ❑ Are search/filter operations accurate?
  ❑ Are pagination calculations correct? (off-by-one errors)
  ❑ Are currency displays locale-appropriate?

COMMON BUGS:
  🐛 $10.10 + $10.20 = $20.299999999 (floating-point)
  🐛 Date shows wrong day because of timezone offset
  🐛 Page 2 shows same items as page 1 (off-by-one)
  🐛 Search finds "apple" but not "Apple" (case sensitivity)
```

### CHECK L4: CRUD Operations
```
WHAT TO CHECK:
  ❑ Create: Duplicate prevention? Loading state? Success feedback?
  ❑ Read: Empty state shown? Pagination? Infinite scroll works?
  ❑ Update: Optimistic updates? Conflict resolution? Stale data?
  ❑ Delete: Confirmation dialog? Undo support? Cascade effects?
  ❑ Is data integrity maintained after each operation?
  ❑ Does the list refresh after create/update/delete?

COMMON BUGS:
  🐛 Double-click creates duplicate record
  🐛 Deleted item still visible until page refresh
  🐛 Update shows success but data doesn't change (stale cache)
  🐛 Empty list shows nothing instead of "No items found"
  🐛 Infinite scroll loads same page repeatedly
```

### CHECK L5: Authentication & Authorization Flow
```
WHAT TO CHECK:
  ❑ Does login redirect to the intended page after auth?
  ❑ Does logout clear all local state/tokens/cookies?
  ❑ Are protected routes guarded both client-side and server-side?
  ❑ Is session timeout handled? (redirect to login with message)
  ❑ Is the registration flow complete? (email verification, password rules)
  ❑ Is "forgot password" implemented securely?
  ❑ Are role-based features properly hidden AND server-validated?

COMMON BUGS:
  🐛 After login, redirects to home instead of the page user wanted
  🐛 Logout doesn't clear localStorage → token persists
  🐛 Admin page hidden in UI but accessible via URL
  🐛 Session expires silently → next action fails with cryptic error
  🐛 Password reset link doesn't expire
```

### CHECK L6: Real-time Features
```
WHAT TO CHECK:
  ❑ Do real-time updates work? (WebSocket, SSE, polling)
  ❑ Is data consistent across multiple tabs?
  ❑ Are optimistic updates rolled back on failure?
  ❑ Is connection loss handled? (reconnection, indicator)
  ❑ Are notifications delivered correctly?

COMMON BUGS:
  🐛 Edit in Tab A not reflected in Tab B
  🐛 WebSocket disconnect shows no indicator
  🐛 Optimistic update stays after server rejects
```

---

## 🚦 PHASE 3 GATE — MANDATORY CHECKLIST

```
PHASE 3 GATE CHECKLIST:
  □ [L1] Input validation verified for all user inputs
  □ [L2] State machine and workflow logic verified
  □ [L3] Calculations and data processing checked
  □ [L4] CRUD operations verified
  □ [L5] Auth/authz flow tested
  □ [L6] Real-time features checked (if applicable)
  □ Minimum 12 code citations provided
  □ Files examined list produced
```
