# Phase 6: Browser & Device Compatibility 🌍

> **Objective:** Verify the web app works correctly across all major browsers and devices.
> A bug that only appears in Safari can affect 25% of your mobile users.

---

## 📋 COMPATIBILITY CHECKS

### CHECK C1: Cross-Browser JavaScript
```
WHAT TO CHECK:
  ❑ Are modern APIs polyfilled for older browsers? (IntersectionObserver, fetch, AbortController)
  ❑ Are ES6+ features transpiled? (optional chaining, nullish coalescing)
  ❑ Is the browserslist configured? (package.json or .browserslistrc)
  ❑ Are Web APIs used with fallbacks? (Clipboard API, Web Share API)
  ❑ Are browser-specific quirks handled?

COMMON BUGS:
  🐛 Optional chaining (?.) crashes in older Safari
  🐛 CSS gap in flexbox not supported in Safari < 14.1
  🐛 Clipboard API fails silently in Firefox (needs user gesture)
  🐛 ResizeObserver loop error in Chrome
  🐛 Date parsing differs between browsers (Date.parse behavior)
```

### CHECK C2: Cross-Browser CSS
```
WHAT TO CHECK:
  ❑ Are vendor prefixes handled? (autoprefixer configured)
  ❑ Are modern CSS features supported? (container queries, :has(), subgrid)
  ❑ Is the CSS reset/normalize applied? (consistent base styles)
  ❑ Are scrollbar styles cross-browser? (Webkit vs Firefox)
  ❑ Do form elements render consistently?

COMMON BUGS:
  🐛 backdrop-filter not working in Firefox without flag
  🐛 Select/dropdown styling breaks on Safari
  🐛 Scrollbar custom styles only work in Chrome
  🐛 :focus-visible not supported in older browsers
```

### CHECK C3: Mobile Browser Testing
```
WHAT TO CHECK:
  ❑ Does the viewport meta tag exist? (<meta name="viewport" ...>)
  ❑ Is the app usable on touch devices? (hover states have alternatives)
  ❑ Is the virtual keyboard handled? (doesn't hide form fields)
  ❑ Are gestures supported? (swipe, pinch-zoom)
  ❑ Does the app work in standalone PWA mode?
  ❑ Is Safari's address bar (100vh issue) handled? (use dvh or svh)

COMMON BUGS:
  🐛 100vh includes Safari address bar → bottom content hidden
  🐛 Hover-only dropdown impossible to use on touch
  🐛 Virtual keyboard pushes content up → layout breaks
  🐛 Fixed position footer jumps on mobile scroll
  🐛 Pinch-zoom disabled (bad accessibility)
```

### CHECK C4: PWA Features
```
WHAT TO CHECK (if PWA):
  ❑ Is manifest.json complete? (name, icons, start_url, display)
  ❑ Is the Service Worker registered correctly?
  ❑ Does offline mode work? (cached shell, offline page)
  ❑ Is the install prompt shown at the right time?
  ❑ Are icons provided in all sizes? (192x192, 512x512)
  ❑ Is the theme-color set?
```

### CHECK C5: Internationalization (i18n)
```
WHAT TO CHECK:
  ❑ Is text externalized for translation?
  ❑ Is RTL layout supported? (Arabic, Hebrew)
  ❑ Are dates/numbers/currencies locale-formatted?
  ❑ Does the layout accommodate longer translated text?
  ❑ Is the html lang attribute set?
```

---

## 🚦 PHASE 6 GATE — MANDATORY CHECKLIST

```
PHASE 6 GATE CHECKLIST:
  □ [C1] Cross-browser JavaScript verified
  □ [C2] Cross-browser CSS checked
  □ [C3] Mobile browser testing assessed
  □ [C4] PWA features verified (if applicable)
  □ [C5] Internationalization checked
  □ Minimum 8 code citations provided
  □ Files examined list produced
```
