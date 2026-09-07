# Changelog

All notable changes to the Web App Tester Skill are documented here.

## [1.2.0] - 2026-09-08

### Added
- **Phase 13: Automated Offensive Security Testing** (`13-automated-offensive-testing.md`)
  - OWASP ZAP automated baseline and full scan
  - Nuclei vulnerability scanning with CVE templates
  - SSL/TLS configuration testing (testssl.sh)
  - Security headers comprehensive audit
  - Dependency vulnerability scanning (npm audit, retire.js, Snyk, Trivy)
  - Web server misconfiguration scanning (nikto)
  - 28 minimum citations from real tool outputs
  - Tool unavailability protocol with manual fallback
- Sentry validation renumbered to Phase 14
- Total minimum citations raised from 91 to 119
- Total phases raised from 13 to 14

## [1.0.0] - 2026-09-06

### Added
- Initial release of the comprehensive web app testing skill
- 13 structured review phases with mandatory gates and STOP points
- Anti-laziness enforcement system with 6 built-in mechanisms:
  - Proof-of-work citations (91 minimum total across all phases)
  - Mandatory phase gate checklists
  - Mandatory STOP points between phases
  - Cross-reference verification matrix in final phase
  - Fresh-Eyes re-analysis (4-layer reminder system for second independent pass)
  - Hacker Mindset R6 post-fix verification from attacker's perspective
- Full OWASP Web Top 10 security coverage: XSS, CSRF, CORS, CSP, cookie security, injection
- Mandatory web search for current-year CVEs in Phase 4 (Security Audit)
- Mandatory web search for current SEO/GDPR policies in Phase 12
- Core Web Vitals analysis (LCP, INP, CLS)
- Support for 16 web frameworks:
  - React, Next.js, Vue, Nuxt, Angular
  - Svelte, SvelteKit, Astro, Remix, Solid, Gatsby
  - PHP/Laravel Blade, Django Templates, Rails ERB
  - ASP.NET Razor, jQuery/Vanilla JS
- Phase 11: Structured Remediation with sprint-based fixes
- Phase 12: SEO & Commercial Readiness (meta tags, Open Graph, payments, GDPR, analytics, PWA)
- Phase 13: Pre-Delivery Sentry Validation (real-browser testing with step-by-step guidance)
- Executive summary with health score (0-100) and release recommendation
- Severity classification system (Critical / High / Medium / Low)
- Framework auto-detection from project files
- Bilingual support (English + Arabic)
