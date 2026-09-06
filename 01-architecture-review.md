# Phase 1: Architecture Review 🏗️

> **Objective:** Analyze the web application's foundational structure, dependencies, routing,
> rendering strategy, and code organization. A bad architecture = guaranteed bugs at scale.

---

## 🔍 PRE-CHECK: Project Discovery

### 1.1 Project Structure Map
```
ACTION: List the ENTIRE project directory tree (at least 3 levels deep)
LOOK FOR:
  - Clear separation: pages/routes, components, services, hooks/composables, utils
  - Test directories present? (tests/, __tests__, *.test.ts, *.spec.ts)
  - Environment configs? (.env, .env.local, .env.production)
  - Build configuration? (vite.config, webpack.config, next.config)
```

### 1.2 Dependency Audit
```
CHECK EACH DEPENDENCY:
  ❑ Still maintained? (last update within 12 months)
  ❑ Known vulnerabilities? (run `npm audit` / `yarn audit` mentally)
  ❑ Version pinned or floating? (^1.0.0 vs 1.0.0)
  ❑ Dev dependencies separated from production?
  ❑ Unnecessary/unused dependencies?
  ❑ Duplicate dependencies? (react-router AND reach-router)
  ❑ Bundle size impact of each dependency?
```

---

## 📋 ARCHITECTURE CHECKS

### CHECK A1: Rendering Strategy
```
WHAT TO CHECK:
  ❑ What rendering strategy is used? (CSR / SSR / SSG / ISR / Hybrid)
  ❑ Is it appropriate for the content type?
    - Blog/docs → SSG ✅ (CSR ❌ bad for SEO)
    - Dashboard → CSR ✅ (SSG ❌ stale data)
    - E-commerce → SSR/ISR ✅ (CSR ❌ bad for SEO + performance)
  ❑ Are dynamic routes properly handled?
  ❑ Is hydration handled correctly? (SSR → client mismatch?)
  ❑ Are meta tags server-rendered? (critical for SEO)

RED FLAGS:
  🔴 CSR-only app that needs SEO (blog, e-commerce, landing page)
  🔴 SSR for everything including dashboard → unnecessary server load
  🔴 Hydration mismatch warnings in console
  🔴 Client-side redirects instead of server-side (flicker)
```

### CHECK A2: Routing Architecture
```
WHAT TO CHECK:
  ❑ Is routing file-based or config-based?
  ❑ Are routes properly organized? (nested, grouped, lazy-loaded)
  ❑ Are protected routes guarded? (auth check before render)
  ❑ Are 404 and error pages implemented?
  ❑ Are route parameters validated?
  ❑ Is there a loading state during route transitions?
  ❑ Are deep links supported and shareable?

COMMON BUGS:
  🐛 Protected page briefly flashes before redirect (no server guard)
  🐛 No 404 page → blank screen for invalid URLs
  🐛 Route parameter not validated → crash on /users/undefined
  🐛 Back button behavior broken after auth redirect
  🐛 Hash routing (#/) breaks SSR and SEO
```

### CHECK A3: Component Architecture
```
WHAT TO CHECK:
  ❑ Is there a clear component hierarchy? (atomic design, feature-based)
  ❑ Are components reusable and composable?
  ❑ Is prop drilling avoided? (use context, stores, or composition)
  ❑ Are components properly sized? (not 500+ lines)
  ❑ Is there a design system or UI library?
  ❑ Are shared components in a common folder?

RED FLAGS:
  🔴 God component with 1000+ lines of logic
  🔴 Props passed through 5+ levels (prop drilling)
  🔴 Business logic inside UI components
  🔴 Inline styles mixed with CSS modules mixed with Tailwind
  🔴 No shared components → everything duplicated
```

### CHECK A4: Build & Bundle Configuration
```
WHAT TO CHECK:
  ❑ Is tree-shaking enabled?
  ❑ Is code splitting configured? (dynamic imports, route-based splits)
  ❑ Are source maps disabled in production?
  ❑ Is minification enabled?
  ❑ Are environment variables properly typed and validated?
  ❑ Is the bundle size reasonable? (< 200KB initial JS for most apps)
  ❑ Are images optimized? (next/image, vite-imagetools)

COMMON BUGS:
  🐛 Entire library imported for one function (import _ from 'lodash')
  🐛 Source maps shipped to production → code exposed
  🐛 No code splitting → 5MB initial bundle
  🐛 process.env used in browser code without NEXT_PUBLIC_ / VITE_ prefix
  🐛 Dev-only code shipped to production (console.logs, debug panels)
```

### CHECK A5: API Layer Architecture
```
WHAT TO CHECK:
  ❑ Is there a centralized API client? (not fetch() scattered everywhere)
  ❑ Are API endpoints typed? (TypeScript interfaces, Zod schemas)
  ❑ Is authentication handled centrally? (interceptors, middleware)
  ❑ Are API routes separated from page routes? (Next.js API routes)
  ❑ Is data fetching colocated with components or centralized?
  ❑ Is caching strategy defined? (SWR, React Query, Apollo Cache)
```

### CHECK A6: Environment & Configuration
```
WHAT TO CHECK:
  ❑ Are environment variables properly prefixed? (NEXT_PUBLIC_, VITE_)
  ❑ Are secrets kept server-side only? (never in NEXT_PUBLIC_ or VITE_)
  ❑ Are there separate .env files per environment?
  ❑ Is .env in .gitignore?
  ❑ Are default values provided for missing env vars?
  ❑ Is there a runtime config validation? (fail fast on missing vars)

RED FLAGS:
  🔴 API secret key in NEXT_PUBLIC_ or VITE_ → exposed to browser
  🔴 .env committed to Git
  🔴 No .env.example for team onboarding
  🔴 Hardcoded URLs that change per environment
```

---

## 🚦 PHASE 1 GATE — MANDATORY CHECKLIST

```
PHASE 1 GATE CHECKLIST:
  □ [A1] Rendering strategy analyzed
  □ [A2] Routing architecture verified
  □ [A3] Component architecture assessed
  □ [A4] Build/bundle configuration checked
  □ [A5] API layer architecture reviewed
  □ [A6] Environment/configuration verified
  □ Dependency audit completed
  □ Project Structure Map produced
  □ Minimum 8 code citations provided
  □ Files examined list produced
```
