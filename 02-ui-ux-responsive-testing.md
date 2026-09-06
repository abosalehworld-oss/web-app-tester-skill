# Phase 2: UI/UX & Responsive Testing 🎨📱

> **Objective:** Test every visual element, interaction, responsive behavior, accessibility
> feature, and animation. Web apps MUST work perfectly from 320px mobile to 4K desktop.

---

## 📋 UI/UX CHECKS

### CHECK U1: Responsive Design
```
WHAT TO CHECK:
  ❑ Does the layout adapt correctly at all breakpoints?
    - 320px (small mobile)
    - 375px (iPhone SE/12 mini)
    - 768px (tablet)
    - 1024px (laptop)
    - 1440px (desktop)
    - 1920px+ (large desktop)
  ❑ Is there horizontal scrolling at any viewport? (should never happen)
  ❑ Are touch targets large enough on mobile? (≥ 44x44px)
  ❑ Does the navigation adapt? (hamburger menu on mobile)
  ❑ Are images responsive? (srcset, picture element, or CSS)
  ❑ Are tables responsive? (horizontal scroll or card layout on mobile)
  ❑ Is text readable at all sizes? (min 16px body text on mobile)

COMMON BUGS:
  🐛 Fixed-width container breaks on mobile
  🐛 Horizontal scroll on mobile (overflowing element)
  🐛 Button too small to tap on mobile (< 44px)
  🐛 Text overflows container on small screens
  🐛 Desktop navigation shows on mobile (no hamburger)
  🐛 Images stretch or pixelate on different screen sizes
```

### CHECK U2: Forms & User Input
```
WHAT TO CHECK:
  ❑ Are all form fields properly labeled? (<label> with htmlFor)
  ❑ Is real-time validation present? (not just on submit)
  ❑ Are error messages displayed clearly near the relevant field?
  ❑ Do inputs have correct types? (email, tel, number, password)
  ❑ Is autocomplete enabled for common fields? (name, email, address)
  ❑ Does Enter submit the form?
  ❑ Is Tab order logical?
  ❑ Are required fields marked?
  ❑ Is the submit button disabled during submission? (prevent double-submit)

COMMON BUGS:
  🐛 Error message far from the field it relates to
  🐛 Form loses all data on validation error (fields cleared)
  🐛 No loading state on submit → user clicks multiple times
  🐛 Password field with autocomplete="off" → poor UX
  🐛 Mobile keyboard doesn't match input type (text keyboard for phone number)
```

### CHECK U3: Accessibility (WCAG 2.1)
```
WHAT TO CHECK:
  ❑ Do all images have meaningful alt text?
  ❑ Are interactive elements keyboard accessible? (Tab, Enter, Escape)
  ❑ Is focus visible on all interactive elements?
  ❑ Are ARIA labels used correctly? (aria-label, aria-describedby, role)
  ❑ Is color contrast sufficient? (≥ 4.5:1 for text, ≥ 3:1 for large text)
  ❑ Does the page have proper heading hierarchy? (h1 → h2 → h3, no skipping)
  ❑ Are form errors announced to screen readers? (aria-live, role="alert")
  ❑ Can modals be closed with Escape?
  ❑ Is focus trapped inside open modals?
  ❑ Do skip links exist? ("Skip to main content")

COMMON BUGS:
  🐛 <div onClick> without role="button" and tabIndex → not keyboard accessible
  🐛 Image with alt="" that contains important information
  🐛 Low contrast text (light gray on white)
  🐛 Modal can't be closed with keyboard
  🐛 Focus goes behind modal to page content
  🐛 Multiple h1 tags on single page
```

### CHECK U4: Navigation & Routing UX
```
WHAT TO CHECK:
  ❑ Is the current page/section highlighted in navigation?
  ❑ Does the back button work correctly?
  ❑ Are breadcrumbs present for nested pages?
  ❑ Is there a loading indicator during page transitions?
  ❑ Do links look like links? (underlined or clearly styled)
  ❑ Are external links marked? (icon or new tab indicator)
  ❑ Is the 404 page helpful? (navigation, search, home link)

COMMON BUGS:
  🐛 Back button returns to wrong page after form submission
  🐛 No loading indicator → user thinks app is frozen
  🐛 Active nav item not highlighted
  🐛 External link opens in same tab → user loses their place
```

### CHECK U5: Typography & Visual Consistency
```
WHAT TO CHECK:
  ❑ Are fonts consistent across the app?
  ❑ Is there a consistent spacing system? (4px/8px grid)
  ❑ Are colors from a defined palette? (no random hex values)
  ❑ Is dark mode supported? (if applicable)
  ❑ Are fonts loaded efficiently? (font-display: swap, preload)
  ❑ Is text truncation handled? (ellipsis, line-clamp)
```

### CHECK U6: Modals, Toasts & Notifications
```
WHAT TO CHECK:
  ❑ Do modals prevent background scrolling?
  ❑ Can modals be closed by clicking overlay, X button, and Escape?
  ❑ Are toasts/notifications non-blocking?
  ❑ Do success/error toasts auto-dismiss?
  ❑ Is there a confirmation dialog for destructive actions?
  ❑ Are multiple toasts stacked properly?
```

### CHECK U7: Animations & Transitions
```
WHAT TO CHECK:
  ❑ Are animations smooth? (60fps, using transform/opacity only)
  ❑ Is prefers-reduced-motion respected?
  ❑ Do animations serve a purpose? (not just decorative)
  ❑ Are loading skeletons used instead of spinners?
  ❑ Are page transitions smooth?
```

---

## 🚦 PHASE 2 GATE — MANDATORY CHECKLIST

```
PHASE 2 GATE CHECKLIST:
  □ [U1] Responsive design verified at all breakpoints
  □ [U2] Forms and user input tested
  □ [U3] Accessibility (WCAG 2.1) reviewed
  □ [U4] Navigation and routing UX verified
  □ [U5] Typography and visual consistency checked
  □ [U6] Modals, toasts, and notifications tested
  □ [U7] Animations and transitions checked
  □ Minimum 12 code citations provided
  □ Files examined list produced
```
