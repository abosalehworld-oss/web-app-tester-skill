# Phase 9: Error & Crash Prevention 🛑

> ⚡ **REMINDER:** After completing this phase, Phase 10 requires a **MANDATORY FRESH-EYES
> RE-ANALYSIS** where you must re-read ALL critical files as a different AI agent.
> Do NOT forget this when you reach Phase 10. It is the MOST IMPORTANT step.

> **Objective:** Ensure the application handles ALL error conditions gracefully.
> A web app crash means a white screen — there's no "crash reporter" to help the user.

---

## 📋 ERROR HANDLING CHECKS

### CHECK E1: Global Error Handling
```
WHAT TO CHECK:
  ❑ Is there a global error boundary? (React ErrorBoundary, Vue errorHandler)
  ❑ Does it show a user-friendly fallback UI? (not a blank page)
  ❑ Does it log the error for debugging?
  ❑ Is there a "Try Again" or "Go Home" button in the error UI?
  ❑ Are unhandled promise rejections caught? (window.onunhandledrejection)
  ❑ Are errors in event handlers caught?

COMMON BUGS:
  🐛 One component error crashes the ENTIRE app (no error boundary)
  🐛 Error boundary shows "Something went wrong" with no actions
  🐛 Unhandled promise rejection → silent failure, broken UI
  🐛 Error in setInterval callback → error repeats infinitely
```

### CHECK E2: Null/Undefined Safety
```
WHAT TO CHECK:
  ❑ Are optional chaining and nullish coalescing used?
  ❑ Are API response fields null-checked before access?
  ❑ Are default values provided for potentially undefined props?
  ❑ Are arrays checked before .map(), .filter(), .find()?
  ❑ Are objects checked before property access?
  ❑ TypeScript strict mode enabled? (strictNullChecks)

COMMON BUGS:
  🐛 Cannot read property 'name' of undefined (missing null check)
  🐛 .map() called on undefined API response
  🐛 Object destructuring on null value → crash
  🐛 TypeScript 'any' type hiding null safety issues
```

### CHECK E3: Network Error Handling
```
WHAT TO CHECK:
  ❑ Are 4xx/5xx responses handled with user-friendly messages?
  ❑ Is network timeout handled? (not hanging forever)
  ❑ Is CORS error caught and explained to user?
  ❑ Are API errors shown near the relevant UI component?
  ❑ Is the error dismissible?

COMMON BUGS:
  🐛 CORS error shows as "Network Error" (unhelpful)
  🐛 500 error shows raw JSON to user
  🐛 Error toast appears and disappears too fast to read
  🐛 Multiple failed requests show stacked identical errors
```

### CHECK E4: Form Error Handling
```
WHAT TO CHECK:
  ❑ Are validation errors shown inline? (near the field)
  ❑ Is server-side validation error mapped back to the correct field?
  ❑ Does the form scroll to the first error?
  ❑ Are errors cleared when the user fixes the input?
  ❑ Is the submit button re-enabled after error?

COMMON BUGS:
  🐛 Server returns error but form shows "success"
  🐛 Generic "Validation failed" without specifying which field
  🐛 Error persists after user fixes the field
  🐛 Submit button stays disabled after server error
```

### CHECK E5: Route/Navigation Errors
```
WHAT TO CHECK:
  ❑ Is there a 404 page for unknown routes?
  ❑ Is there a generic error page for unexpected errors?
  ❑ Are route guards handling unauthorized access?
  ❑ Are dynamic route parameters validated?
  ❑ Is lazy-loaded route chunk failure handled? (ChunkLoadError retry)

COMMON BUGS:
  🐛 Unknown URL shows blank page instead of 404
  🐛 /users/abc crashes because ID is not a number
  🐛 Lazy-loaded route fails after deployment → white screen (chunk hash changed)
  🐛 Unauthorized access shows error instead of redirecting to login
```

### CHECK E6: Third-Party Integration Errors
```
WHAT TO CHECK:
  ❑ Are payment gateway errors handled? (Stripe, PayPal failures)
  ❑ Are social login failures handled? (OAuth errors)
  ❑ Are map/chart library errors caught?
  ❑ Are analytics failures silent? (should not break app)
  ❑ Are CDN failures handled? (fallback fonts, local assets)

COMMON BUGS:
  🐛 Stripe.js fails to load → payment page crashes
  🐛 Google Maps API key expired → blank map, no error message
  🐛 Analytics script blocked by ad blocker → app crashes
  🐛 OAuth popup blocked → no feedback to user
```

---

## 🚦 PHASE 9 GATE — MANDATORY CHECKLIST

```
PHASE 9 GATE CHECKLIST:
  □ [E1] Global error handling verified
  □ [E2] Null/undefined safety checked
  □ [E3] Network error handling assessed
  □ [E4] Form error handling verified
  □ [E5] Route/navigation errors checked
  □ [E6] Third-party integration errors handled
  □ Minimum 10 code citations provided
  □ Files examined list produced
```
