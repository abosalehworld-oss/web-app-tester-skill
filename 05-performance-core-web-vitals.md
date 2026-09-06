# Phase 5: Performance & Core Web Vitals ⚡

> **Objective:** Analyze performance bottlenecks affecting user experience and SEO ranking.
> Google uses Core Web Vitals as a ranking signal — poor performance = lower search results.

---

## 📋 PERFORMANCE CHECKS

### CHECK P1: Core Web Vitals
```
WHAT TO CHECK:
  ❑ LCP (Largest Contentful Paint) — target < 2.5s
    - Is the largest element (hero image, heading) rendered quickly?
    - Are fonts loaded with font-display: swap?
    - Are above-the-fold images prioritized? (loading="eager", fetchpriority="high")
  ❑ FID/INP (Interaction to Next Paint) — target < 200ms
    - Are click handlers fast? (no heavy computation on main thread)
    - Is JavaScript execution blocking interactions?
  ❑ CLS (Cumulative Layout Shift) — target < 0.1
    - Do images/ads/embeds have explicit width/height?
    - Do dynamic elements (banners, notifications) push content?
    - Do fonts cause layout shift when loaded?

COMMON BUGS:
  🐛 Hero image loads last (no priority hint) → LCP = 5s
  🐛 Font swap causes text to jump → CLS spike
  🐛 Ad banner inserts above content → pushes everything down
  🐛 Click handler runs 500ms computation → INP failure
```

### CHECK P2: JavaScript Bundle Size
```
WHAT TO CHECK:
  ❑ Is the initial JS bundle < 200KB (gzipped)?
  ❑ Is code splitting implemented? (route-based, component-based)
  ❑ Are heavy libraries lazy-loaded? (charts, editors, maps)
  ❑ Are barrel exports avoided? (import { x } from '@/utils' imports everything)
  ❑ Is tree-shaking working? (no dead code in bundle)
  ❑ Are polyfills targeted? (not polyfilling for modern browsers)

COMMON BUGS:
  🐛 moment.js imported (300KB) when day.js (2KB) suffices
  🐛 Entire icon library imported for 3 icons
  🐛 import * from 'lodash' instead of import { debounce } from 'lodash/debounce'
  🐛 Development-only code in production bundle
```

### CHECK P3: Image Optimization
```
WHAT TO CHECK:
  ❑ Are images in modern formats? (WebP, AVIF)
  ❑ Are images responsive? (srcset with multiple sizes)
  ❑ Are offscreen images lazy-loaded? (loading="lazy")
  ❑ Are images properly sized? (not serving 4000px image in 400px container)
  ❑ Is a CDN used for image delivery?
  ❑ Are SVGs used for icons/illustrations? (not PNGs for simple shapes)

COMMON BUGS:
  🐛 5MB JPEG used as background image
  🐛 All images loaded eagerly (no lazy loading)
  🐛 Same image served at 4000px for 200px thumbnail
```

### CHECK P4: Caching Strategy
```
WHAT TO CHECK:
  ❑ Are static assets cached? (Cache-Control, ETag)
  ❑ Are hashed filenames used for cache busting?
  ❑ Is a Service Worker caching strategy defined? (if PWA)
  ❑ Are API responses cached appropriately? (SWR, stale-while-revalidate)
  ❑ Is CDN caching configured?

COMMON BUGS:
  🐛 No cache headers → browser re-downloads everything on each visit
  🐛 Cache-Control: no-cache on static assets
  🐛 API cache never invalidated → stale data
```

### CHECK P5: Rendering Performance
```
WHAT TO CHECK:
  ❑ Are lists virtualized? (react-virtual, vue-virtual-scroller for 100+ items)
  ❑ Are expensive re-renders prevented? (React.memo, useMemo, computed)
  ❑ Are CSS animations using transform/opacity? (not width/height/top/left)
  ❑ Is the DOM size reasonable? (< 1500 nodes)
  ❑ Are third-party scripts deferred? (analytics, chat widgets)

COMMON BUGS:
  🐛 Table with 10K rows rendered at once → browser freezes
  🐛 Every keystroke in search re-renders entire list (no debounce)
  🐛 CSS animation on 'left' property → layout thrashing
  🐛 Google Analytics script blocks rendering
```

### CHECK P6: Network Optimization
```
WHAT TO CHECK:
  ❑ Are critical resources preloaded? (<link rel="preload">)
  ❑ Is DNS prefetch used for external domains?
  ❑ Are API calls batched where possible?
  ❑ Is HTTP/2 or HTTP/3 used?
  ❑ Is compression enabled? (gzip/brotli)
  ❑ Are unnecessary redirects eliminated?
```

---

## 🚦 PHASE 5 GATE — MANDATORY CHECKLIST

```
PHASE 5 GATE CHECKLIST:
  □ [P1] Core Web Vitals analyzed (LCP, INP, CLS)
  □ [P2] JavaScript bundle size checked
  □ [P3] Image optimization verified
  □ [P4] Caching strategy reviewed
  □ [P5] Rendering performance assessed
  □ [P6] Network optimization checked
  □ Minimum 8 code citations provided
  □ Files examined list produced
```
