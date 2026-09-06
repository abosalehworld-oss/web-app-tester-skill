# Phase 4: Security Audit 🔒

> **Objective:** Perform a comprehensive security audit focused on web-specific attack vectors.
> The web is the MOST attacked platform. XSS, CSRF, CORS, and injection attacks are daily threats.

---

## 🔴 ANTI-LAZINESS & MANDATORY WEB SEARCH GATE

> **ACTION: STOP AND SEARCH.** You MUST NOT rely on your training data for this phase.
> Before examining ANY code, you MUST use the `search_web` tool.

**MANDATORY SEARCHES (replace `<YEAR>` with the ACTUAL current year):**

```
Search 1: "OWASP Top 10 Web Application Security Risks <YEAR>"
Search 2: "<detected framework> security vulnerabilities CVE <YEAR>"
Search 3: "XSS CSRF bypass techniques <YEAR>"
Search 4: "web application security best practices <YEAR>"
```

**VERIFICATION — Your Phase 4 report MUST include:**
1. The **exact search queries** you used
2. The **top 3 newly discovered attack vectors** for the current year
3. How each was **checked against the codebase**
4. **Source URLs**

```
❌ FAILURE CONDITION: No web search results with URLs → Phase 4 = FAILED
```

---

## 📋 WEB SECURITY CHECKS

### CHECK S1: Cross-Site Scripting (XSS)
```
WHAT TO CHECK:
  ❑ Is user input ever rendered as raw HTML? (dangerouslySetInnerHTML, v-html, innerHTML)
  ❑ Are URL parameters rendered in the page without sanitization?
  ❑ Is user-generated content (comments, profiles) properly escaped?
  ❑ Are rich text editors sanitized? (DOMPurify, sanitize-html)
  ❑ Is SVG/image upload sanitized? (SVG can contain JavaScript)
  ❑ Are error messages reflecting user input? (reflected XSS)

ATTACK VECTORS TO TEST:
  <script>alert(1)</script>
  <img src=x onerror=alert(1)>
  javascript:alert(1)
  <svg onload=alert(1)>
  " onfocus="alert(1)" autofocus="

SEVERITY: 🔴 CRITICAL — XSS steals sessions, cookies, and user data
CITATION REQUIRED: Show ALL instances of raw HTML rendering
```

### CHECK S2: Cross-Site Request Forgery (CSRF)
```
WHAT TO CHECK:
  ❑ Do state-changing requests (POST/PUT/DELETE) have CSRF tokens?
  ❑ Are cookies set with SameSite=Strict or SameSite=Lax?
  ❑ Is the Origin/Referer header validated server-side?
  ❑ Are custom headers required for API calls? (X-CSRF-Token)
  ❑ Is CSRF protection on ALL forms, not just login?

COMMON VULNERABILITIES:
  🔴 Form submission without CSRF token → attacker crafts auto-submit page
  🔴 API accepts requests without Origin validation
  🔴 SameSite cookie not set → cookie sent from attacker's site

SEVERITY: 🔴 CRITICAL
CITATION REQUIRED: Show form submissions and cookie configurations
```

### CHECK S3: CORS Misconfiguration
```
WHAT TO CHECK:
  ❑ Is Access-Control-Allow-Origin set to specific domains? (NOT *)
  ❑ Is Access-Control-Allow-Credentials: true with specific origin? (NOT *)
  ❑ Are allowed methods restricted? (not all methods)
  ❑ Are allowed headers restricted?
  ❑ Is the origin validated against a whitelist?

COMMON VULNERABILITIES:
  🔴 Access-Control-Allow-Origin: * with credentials → any site reads data
  🔴 Origin reflected from request → CORS bypass
  🔴 Null origin allowed → attackers use sandbox iframes

SEVERITY: 🔴 CRITICAL
CITATION REQUIRED: Show CORS configuration
```

### CHECK S4: Content Security Policy (CSP)
```
WHAT TO CHECK:
  ❑ Is a CSP header set?
  ❑ Does it block unsafe-inline for scripts?
  ❑ Does it block unsafe-eval?
  ❑ Is frame-ancestors set? (prevents clickjacking)
  ❑ Is the policy not too permissive? (not *)
  ❑ Are nonces or hashes used for inline scripts?

RED FLAGS:
  🟠 No CSP header at all
  🟠 CSP with 'unsafe-inline' and 'unsafe-eval' → defeats XSS protection
  🟠 CSP with wildcard sources (*.cdn.com)
  🟠 No frame-ancestors → clickjacking possible

SEVERITY: 🟠 HIGH
CITATION REQUIRED: Show CSP header configuration
```

### CHECK S5: Cookie Security
```
WHAT TO CHECK:
  ❑ Are auth cookies HttpOnly? (JavaScript can't read them)
  ❑ Are auth cookies Secure? (HTTPS only)
  ❑ Are cookies SameSite=Strict or Lax?
  ❑ Is cookie expiry appropriate? (not 10 years)
  ❑ Are sensitive values encrypted in cookies?
  ❑ Is cookie consent implemented? (GDPR)

COMMON VULNERABILITIES:
  🔴 Auth token in non-HttpOnly cookie → stolen via XSS
  🔴 Cookie without Secure flag → sent over HTTP
  🔴 Session cookie with no expiry → permanent session hijacking

SEVERITY: 🔴 CRITICAL for auth cookies
CITATION REQUIRED: Show ALL cookie configurations
```

### CHECK S6: Authentication Security
```
WHAT TO CHECK:
  ❑ Are passwords hashed server-side? (bcrypt, argon2 — NOT MD5/SHA1)
  ❑ Is rate limiting on login? (brute-force protection)
  ❑ Is JWT stored securely? (HttpOnly cookie, NOT localStorage)
  ❑ Is token refresh implemented?
  ❑ Are OAuth redirect URIs strictly validated?
  ❑ Is 2FA available for sensitive operations?
  ❑ Are password reset tokens single-use and time-limited?

COMMON VULNERABILITIES:
  🔴 JWT in localStorage → stolen via XSS
  🔴 No rate limiting → brute-force login
  🔴 Password reset link never expires
  🔴 OAuth open redirect → token theft

SEVERITY: 🔴 CRITICAL
CITATION REQUIRED: Show auth flow, token storage, and session management
```

### CHECK S7: Injection Attacks
```
WHAT TO CHECK:
  ❑ SQL Injection: Are queries parameterized? (no string concatenation)
  ❑ NoSQL Injection: Are MongoDB queries using user input safely?
  ❑ Command Injection: Is any user input passed to exec/spawn?
  ❑ Template Injection: Is user input rendered in server templates?
  ❑ Header Injection: Is user input used in HTTP headers?
  ❑ Open Redirect: Are redirect URLs validated against whitelist?

SEVERITY: 🔴 CRITICAL for SQL/command injection
CITATION REQUIRED: Show ALL database queries and external command execution
```

### CHECK S8: Security Headers
```
WHAT TO CHECK:
  ❑ X-Content-Type-Options: nosniff
  ❑ X-Frame-Options: DENY or SAMEORIGIN
  ❑ Strict-Transport-Security (HSTS)
  ❑ Referrer-Policy: strict-origin-when-cross-origin
  ❑ Permissions-Policy: (camera, microphone, geolocation)
  ❑ X-XSS-Protection: 0 (deprecated, CSP is better)

SEVERITY: 🟠 HIGH for missing HSTS, 🟡 MEDIUM for others
CITATION REQUIRED: Show response headers configuration
```

### CHECK S9: Sensitive Data Exposure
```
WHAT TO CHECK:
  ❑ Are API keys exposed in client-side code?
  ❑ Are secrets in JavaScript bundle? (search for key patterns)
  ❑ Are error messages leaking stack traces to users?
  ❑ Is sensitive data in URL parameters? (logged in server access logs)
  ❑ Are source maps disabled in production?
  ❑ Is .env committed to the repository?
  ❑ Are console.log statements removed from production?

SEVERITY: 🔴 CRITICAL for API keys, 🟠 HIGH for others
CITATION REQUIRED: Show any exposed secrets or sensitive data
```

### CHECK S10: File Upload Security
```
WHAT TO CHECK:
  ❑ Is file type validated server-side? (not just client extension)
  ❑ Is file size limited?
  ❑ Are uploaded files stored outside the web root?
  ❑ Are filenames sanitized? (path traversal prevention)
  ❑ Is antivirus scanning implemented for uploads?
  ❑ Are uploaded images re-processed? (strip EXIF, re-encode)

SEVERITY: 🔴 CRITICAL for missing server validation
```

---

## 🚦 PHASE 4 GATE — MANDATORY CHECKLIST

```
PHASE 4 GATE CHECKLIST:
  □ [S1] XSS verified across all user content rendering
  □ [S2] CSRF protection checked on all forms
  □ [S3] CORS configuration reviewed
  □ [S4] CSP header checked
  □ [S5] Cookie security verified
  □ [S6] Authentication security reviewed
  □ [S7] Injection attacks assessed
  □ [S8] Security headers checked
  □ [S9] Sensitive data exposure reviewed
  □ [S10] File upload security verified (if applicable)
  □ Web search results included with URLs
  □ Current-year attack vectors checked
  □ Minimum 15 code citations provided
  □ Files examined list produced
```
