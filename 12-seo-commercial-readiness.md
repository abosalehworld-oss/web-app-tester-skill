# Phase 12: SEO & Commercial Readiness 🔍💰

> **Objective:** Verify the web app is ready for search engines, commercial use,
> and legal compliance. SEO and GDPR mistakes cost traffic, revenue, and legal risk.

---

## 🔴 MANDATORY WEB SEARCH (Rule 9)

Before completing this phase, you MUST search:

```
Search 1: "Google SEO ranking factors <current year>"
Search 2: "Core Web Vitals SEO impact <current year>"
Search 3: "GDPR cookie consent requirements <current year>"
Search 4: "web accessibility legal requirements <current year>"
Search 5: "<detected framework> SEO best practices <current year>"
```

**Include URLs in your report.**

---

## 📋 SEO & COMMERCIAL CHECKS

### CHECK R1: Technical SEO
```
WHAT TO CHECK:
  ❑ Does every page have a unique <title> tag?
  ❑ Does every page have a <meta name="description">?
  ❑ Is there a proper heading hierarchy? (one h1 per page)
  ❑ Are images using alt text?
  ❑ Is a sitemap.xml generated?
  ❑ Is robots.txt configured correctly?
  ❑ Are canonical URLs set? (<link rel="canonical">)
  ❑ Is the site HTTPS only? (redirect HTTP → HTTPS)
  ❑ Are structured data/JSON-LD schemas present?
  ❑ Is server-side rendering enabled for SEO pages?

COMMON BUGS:
  🐛 All pages have the same <title> → Google shows duplicate titles
  🐛 SPA with no SSR → Google can't index content
  🐛 Missing sitemap → Google discovers pages slowly
  🐛 robots.txt blocks important pages
  🐛 No canonical URL → duplicate content penalty
```

### CHECK R2: Open Graph & Social Media
```
WHAT TO CHECK:
  ❑ Are og:title, og:description, og:image set?
  ❑ Are Twitter Card meta tags set?
  ❑ Is og:image the right size? (1200x630 for Facebook)
  ❑ Are dynamic pages generating correct OG tags?
  ❑ Is the favicon set? (favicon.ico + apple-touch-icon)

COMMON BUGS:
  🐛 Sharing on Facebook/Twitter shows no image or wrong image
  🐛 OG tags are static on all pages (same title everywhere)
  🐛 OG image too small or wrong aspect ratio
```

### CHECK R3: Payment Integration
```
WHAT TO CHECK (if applicable):
  ❑ Is the payment flow using Stripe/PayPal official SDKs?
  ❑ Is price calculated server-side? (not from client request)
  ❑ Are payment webhooks verified? (signature validation)
  ❑ Is the payment page on HTTPS?
  ❑ Are payment errors handled gracefully?
  ❑ Is PCI DSS compliance maintained? (no card data on your servers)
  ❑ Are refund flows implemented?
  ❑ Are receipt/confirmation emails sent?

RED FLAGS:
  🔴 Price sent from client → attacker changes price to $0
  🔴 Webhook without signature verification → fake payment confirmations
  🔴 Card data stored on your server → PCI violation
  🔴 No HTTPS on payment page → data intercepted
```

### CHECK R4: Analytics & Tracking
```
WHAT TO CHECK:
  ❑ Is analytics implemented? (GA4, Plausible, Mixpanel)
  ❑ Is analytics loaded asynchronously? (doesn't block rendering)
  ❑ Are custom events tracked? (sign-up, purchase, feature usage)
  ❑ Is analytics consent obtained before tracking? (GDPR)
  ❑ Does ad blocker not break the app? (analytics failure handled)

COMMON BUGS:
  🐛 Analytics script blocks page load
  🐛 App crashes when ad blocker blocks analytics
  🐛 Tracking without consent → GDPR fine
  🐛 Page views not tracked on SPA navigation (only initial load)
```

### CHECK R5: Cookie Consent & GDPR/CCPA
```
WHAT TO CHECK:
  ❑ Is a cookie consent banner shown? (before setting non-essential cookies)
  ❑ Can the user reject all cookies?
  ❑ Are cookie preferences saved and respected?
  ❑ Is there a privacy policy page?
  ❑ Is there a "Delete My Account" feature? (GDPR right to erasure)
  ❑ Is data collection disclosed?
  ❑ Are third-party cookies declared?

RED FLAGS:
  🟠 Cookies set before consent → GDPR violation
  🟠 No reject option → only "Accept All"
  🟠 No privacy policy → legal risk and store rejection
```

### CHECK R6: Advertising Integration
```
WHAT TO CHECK (if applicable):
  ❑ Are ads loaded asynchronously? (doesn't block content)
  ❑ Are ads positioned without causing layout shift? (CLS)
  ❑ Is ad blocker detection handled? (non-aggressively)
  ❑ Are ads labeled as "Advertisement"?
  ❑ Do ads not cover content? (no accidental clicks)
  ❑ Are ad networks compliant? (Google AdSense policies)
```

### CHECK R7: PWA Readiness
```
WHAT TO CHECK (if applicable):
  ❑ Does the app pass Lighthouse PWA audit?
  ❑ Is the manifest.json complete?
  ❑ Is offline mode functional?
  ❑ Is the install experience smooth?
  ❑ Are push notifications properly permission-gated?
```

---

## 🚦 PHASE 12 GATE — MANDATORY CHECKLIST

```
PHASE 12 GATE CHECKLIST:
  □ [R1] Technical SEO verified
  □ [R2] Open Graph and social media checked
  □ [R3] Payment integration reviewed (if applicable)
  □ [R4] Analytics and tracking verified
  □ [R5] Cookie consent and GDPR checked
  □ [R6] Advertising integration reviewed (if applicable)
  □ [R7] PWA readiness checked (if applicable)
  □ Web search results included with URLs
  □ Files examined list produced
```
