# Phase 11: Structured Remediation 🔧

> **Objective:** Execute code fixes for all findings in a structured, verifiable manner.
> Every fix must be PROVEN with before/after code.

---

### ⚠️ MANDATORY POST-FIX VERIFICATION
After EVERY code modification, you MUST:
1. Call `view_file` on the modified file to confirm your edit was applied correctly
2. Run the project's build command (if available) to verify no syntax/compilation errors
3. Run the project's test suite (if available) to verify no regressions
4. If any verification fails, fix the issue BEFORE proceeding to the next fix

❌ Claiming "fixed" without view_file verification = UNVERIFIED = POTENTIALLY BROKEN

## ⚠️ CRITICAL RULES FOR REMEDIATION

### Rule R1: NO SILENT FIXES
Every fix MUST include: Finding ID, Before code, After code, Why, Risk assessment.

### Rule R2: SPRINT-BASED EXECUTION
1. **Sprint 1 (BLOCKER)** — All 🔴 Critical
2. **Sprint 2 (HIGH)** — All 🟠 High
3. **Sprint 3 (MEDIUM)** — All 🟡 Medium
4. **Backlog (LOW)** — All 🔵 Low

```
🚫 Cannot fix Sprint 2 before ALL Sprint 1 items are done.
🚫 Cannot mark a fix as "done" without showing the diff.
```

### Rule R3: ONE FIX AT A TIME
Each fix: Isolated, Reviewable, Reversible.

### Rule R4: STOP AFTER EACH SPRINT
After completing a sprint → output report → STOP and wait for user confirmation.

### Rule R5: NEW CODE MUST PASS PHASE CHECKS
```
For each fix, verify the NEW code against:

  Security fix (Phase 4):
    ❑ Does new code introduce XSS?
    ❑ Does new code break CSRF protection?
    ❑ Is new input properly sanitized?
    ❑ Are cookies still secure?

  Performance fix (Phase 5):
    ❑ Does new code increase bundle size?
    ❑ Does new code cause re-renders?
    ❑ Does new code block main thread?

  Data fix (Phase 8):
    ❑ Does new code handle null/undefined?
    ❑ Does new code preserve state correctly?
    ❑ Does new code break URL state?
```

### Rule R6: HACKER MINDSET POST-FIX VERIFICATION
After completing ALL sprint fixes, switch to "Ethical Hacker" perspective:

```
For EVERY file modified during remediation:
  ❑ 1. Can I bypass the fix by providing unexpected input?
  ❑ 2. Does the fix handle ALL edge cases? (null, empty, XSS payloads)
  ❑ 3. Does the fix create a new timing/race condition?
  ❑ 4. Does the fix leak information in error messages?
  ❑ 5. If this fix touches auth → can the token still be stolen?
  ❑ 6. If this fix touches forms → is XSS still possible via another vector?
  ❑ 7. Does the fix introduce a new dependency? → Is it secure?
  ❑ 8. Can the fix be circumvented via browser DevTools?
  ❑ 9. Does the fix break existing security controls?
  ❑ 10. Would a penetration tester find this fix adequate?
```

**R6 Report Format:**
```markdown
### 🔍 Rule R6 — Hacker Mindset Verification Report

| File Modified | R6 Result | New Issues |
|--------------|-----------|-----------|
| `path/file` | ✅ SECURE / ⚠️ CONCERN | [desc or NONE] |

**Overall R6 Verdict:** ✅ All fixes verified / ⚠️ [N] concerns → must address
```

---

## 🔁 POST-FIX RE-ANALYSIS

```
After ALL sprints completed:
- [ ] Re-run ALL 9 analysis Phases on modified files
- [ ] Produce new Phase 10 report
- [ ] Confirm ZERO 🔴 Critical and ZERO 🟠 High remain
- [ ] If NEW issues → back to Phase 11 Sprint 1

> THE CYCLE DOES NOT END UNTIL RE-ANALYSIS IS 100% CLEAN.
```

---

## ⛔ ANTI-PREMATURE-CELEBRATION RULE

> **Phase 11 is the REMEDIATION phase ONLY — NOT the final phase.**
> There are still remaining phases after this one (Phase 12: SEO & Commercial Readiness, Phase 13: Pre-Delivery Sentry Validation).
> **Do NOT declare the project "done", "production-ready", or "ready for deployment" after completing Phase 11.**
> You MUST continue to the next phase and await user confirmation before proceeding.

---

## 💡 OPTIONAL: Run Actual Analysis Tools

> If execution tools are available in your environment, prefer running actual commands over mental simulation:
> - `npm audit` / `yarn audit` / `pnpm audit` (Dependencies)
> - `npm run build` / `yarn build` (Build verification)
> - `npx eslint .` / `npx tsc --noEmit` (Linting/Type-checking)
> - `npx lighthouse` (Performance/SEO audit)
>
> If these tools are NOT available, document this limitation in the sprint report.
