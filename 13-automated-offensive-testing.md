# Phase 13: Automated Offensive Security Testing 🔴

> **Objective:** Replace manual penetration testing with automated AI-driven offensive security tools.
> The AI agent installs, configures, runs, and analyzes results from real security testing tools
> that actively attack the web application — not just read its code. This is the DYNAMIC testing layer
> that complements the static analysis performed in Phases 1-12.

---

## ⚠️ IMPORTANT: This Phase is NON-NEGOTIABLE

> This phase uses **real security tools** that perform **actual security assessments** against your web application.
> It is NOT static analysis — it is dynamic offensive testing using industry-standard open-source tools.
> **Do NOT skip this phase.** Do NOT claim "tools are unavailable" without attempting installation first.

---

## 🚨 ANTI-CHEATING RULES FOR THIS PHASE

### Rule OT-A: MANDATORY `run_command` PROOF
> Every tool execution MUST be performed via an actual `run_command` / terminal tool call.
> You MUST show the **real terminal output** — not text you wrote from memory.
> **Writing fake tool output = CHEATING.** If you cannot run the command, mark as MANUAL_CHECK.
> The user can verify by checking the tool call history in the conversation.

### Rule OT-B: MAXIMUM 2 MANUAL_CHECK ALLOWED
> You may mark **at most 2 checks** as MANUAL_CHECK due to tool unavailability.
> If 3 or more tools fail to install, you MUST troubleshoot or try alternative installation
> methods (pip, npm, brew, choco, scoop, docker, direct download).
> **Claiming all tools are unavailable = PHASE INVALID. Start over.**

### Rule OT-C: HACKER MINDSET R6 ON ALL FIXES
> If you fix any finding in this phase, you MUST apply Rule R6 (Hacker Mindset Verification):
> 1. Can the fix be bypassed?
> 2. Does the fix create a new vulnerability?
> 3. Would a penetration tester find this fix adequate?
> **No R6 verification = fix is NOT accepted.**

### Rule OT-D: MANDATORY DATABASE FRESHNESS
> Before running ANY scan, you MUST update the tool's vulnerability database first.
> Run these update commands and show the output:
> ```
> # Nuclei templates (updated weekly with new CVEs)
> nuclei -update-templates
> # nikto database
> nikto -update
> # ZAP add-ons (pull latest Docker image)
> docker pull ghcr.io/zaproxy/zaproxy:stable
> # retire.js database
> npm update -g retire
> ```
> You MUST also run a **web search** for "latest [tool-name] version [current-year]" to verify
> you are using the most current version. Scanning with outdated databases = scanning blind.
> **If the database update fails, document the error and mark the check as PARTIAL.**

### Rule OT-E: MANDATORY FALSE POSITIVE TRIAGE (BEFORE ANY FIX)
> ⚠️ **This is the MOST CRITICAL safety rule in this phase.**
> Automated security tools produce **FALSE POSITIVES** (fake alerts). Blindly fixing a false
> positive can **BREAK the application** — disable login, corrupt data, or block real users.
>
> **BEFORE fixing ANY finding from ANY tool, you MUST complete this triage for EACH finding:**
>
> **Step 1 — Classify the finding:**
> ```
> | Finding ID | Tool | Verdict | Confidence | Reason |
> |------------|------|---------|------------|--------|
> | OT1-F1 | ZAP | TRUE_POSITIVE / FALSE_POSITIVE / UNCERTAIN | HIGH/MEDIUM/LOW | Why? |
> ```
>
> **Step 2 — MANDATORY WEB SEARCH per finding (ANTI-STALE-KNOWLEDGE):**
> Your training data is OUTDATED. You MUST NOT classify findings based on memory alone.
> For EACH finding, run a web search:
> ```
> search_web("[CVE-ID or vulnerability name] false positive [tool-name] [current-year]")
> search_web("[vulnerability name] [framework/library version] exploit proof of concept [current-year]")
> ```
> - If the internet says this CVE is **confirmed exploitable** in the detected version → TRUE_POSITIVE
> - If the internet says this is a **known false positive** for this tool/version → FALSE_POSITIVE
> - If no clear internet consensus exists → UNCERTAIN (present to user with extra caution)
> **DO NOT trust your training data over live internet results. Your knowledge may be 1-2 years stale.**
>
> **Step 3 — For each TRUE_POSITIVE or UNCERTAIN finding, explain in PLAIN LANGUAGE:**
> ```
> 🔴 FINDING: [Tool] reported [vulnerability name]
> 📍 WHERE: [file:line or endpoint]
> 👶 EXPLAIN LIKE I'M 5: [How can a hacker exploit this? What damage can they do?]
> 🔧 PROPOSED FIX: [What exactly will you change in the code?]
> ⚠️ FIX SIDE EFFECTS: [Will this fix break any feature? Will users notice anything different?]
> 🤔 FALSE POSITIVE RISK: [What is the probability this is a false alarm? Why?]
> 🌐 WEB SEARCH EVIDENCE: [What did the internet say about this CVE/vulnerability?]
> ```
>
> **Step 4 — Present the FULL triage table to the user and STOP.**
> ```
> ⛔ STOP — Do NOT fix anything until the user reviews this triage and says "fix" or "skip" for each finding.
> ```
>
> **FORBIDDEN behaviors:**
> ```
> ❌ NEVER fix a finding without completing the triage table first
> ❌ NEVER say "I fixed 5 vulnerabilities" without user approval on EACH one
> ❌ NEVER assume the user understands security jargon — ALWAYS use plain language
> ❌ NEVER hide the false positive probability — the user NEEDS this to make a decision
> ❌ NEVER batch-fix all findings at once — present them individually for approval
> ❌ NEVER classify a finding as FALSE_POSITIVE without a web search proving it
> ❌ NEVER classify a finding as TRUE_POSITIVE without a web search confirming it
> ```
>
> **WHY THIS EXISTS:** The user operating this skill may NOT be a cybersecurity expert.
> They rely on YOUR analysis to decide what to fix. If you fix a false positive, you may
> break their application. If you skip a true positive, you leave them vulnerable.
> Your training data may be outdated — a vulnerability you "remember" as harmless may now
> have a working exploit. The web search requirement ensures you use CURRENT intelligence.
> **Your triage is the user's ONLY defense. Take it seriously.**

---

## 🛠️ TOOL INSTALLATION

Before running any tests, install the required tools:

```bash
# OWASP ZAP - Web Application Security Scanner (Docker recommended)
docker pull ghcr.io/zaproxy/zaproxy:stable
# Or download from: https://www.zaproxy.org/download/

# Nuclei - Fast Vulnerability Scanner
go install -v github.com/projectdiscovery/nuclei/v3/cmd/nuclei@latest
# Or: brew install nuclei / choco install nuclei

# nikto - Web Server Scanner
apt install nikto   # Debian/Ubuntu
brew install nikto  # macOS

# testssl.sh - SSL/TLS Configuration Tester
git clone https://github.com/drwetter/testssl.sh.git

# retire.js - Known Vulnerable JS Library Detection
npm install -g retire
```

---

## 📋 PHASE 13 CHECKS

### [OT1] OWASP ZAP Baseline Scan
```
Action: Run ZAP automated baseline scan against the web application
Commands:
  # Docker (headless baseline scan)
  docker run -t ghcr.io/zaproxy/zaproxy:stable zap-baseline.py -t https://[target-url]
  # Full active scan (more thorough)
  docker run -t ghcr.io/zaproxy/zaproxy:stable zap-full-scan.py -t https://[target-url]
Analyze:
  - XSS vulnerabilities detected
  - SQL Injection points
  - Missing CSRF tokens
  - Missing security headers
  - Missing cookie security flags
  - Information disclosure
  - Directory browsing enabled
  - Path traversal vulnerabilities
Minimum citations: 8 findings from ZAP output
```

### [OT2] Nuclei Vulnerability Scan
```
Action: Run Nuclei with web vulnerability templates
Commands:
  nuclei -u https://[target-url] -t cves/ -t vulnerabilities/ -t exposures/ -t misconfiguration/
  nuclei -u https://[target-url] -t http/technologies/ -t http/exposed-panels/
Analyze:
  - Known CVEs affecting the stack
  - Exposed admin panels
  - Default credentials
  - Misconfigured services
  - Information leakage endpoints
  - Exposed .env / .git / debug endpoints
Minimum citations: 5 findings from Nuclei output
```

### [OT3] SSL/TLS Security Testing
```
Action: Test SSL/TLS configuration of the deployed site
Commands:
  ./testssl.sh https://[target-url]
  # Or use nmap:
  nmap --script ssl-enum-ciphers -p 443 [target-host]
Analyze:
  - TLS version support (must reject TLS 1.0/1.1)
  - Cipher suite strength
  - Certificate chain validity
  - HSTS header presence and max-age
  - OCSP stapling
  - Certificate transparency
Minimum citations: 4 findings
```

### [OT4] Security Headers Audit
```
Action: Verify all security headers are present and correctly configured
Commands:
  curl -sI https://[target-url] | grep -iE "(strict-transport|content-security|x-frame|x-content|referrer-policy|permissions-policy)"
Analyze:
  - Strict-Transport-Security (HSTS)
  - Content-Security-Policy (CSP)
  - X-Frame-Options
  - X-Content-Type-Options
  - Referrer-Policy
  - Permissions-Policy
Minimum citations: 4 findings
```

### [OT5] Dependency Vulnerability Scan
```
Action: Scan all frontend and backend dependencies for known CVEs
Commands:
  npm audit --json      # or yarn audit / pnpm audit
  npx retire --js       # Scan for known vulnerable JS libraries in the bundle
  npx snyk test         # Snyk vulnerability scanner
  trivy fs --security-checks vuln /path/to/project
Analyze:
  - Critical CVEs in dependencies
  - Outdated packages with known exploits
  - Client-side libraries with XSS vulnerabilities
  - Transitive dependency vulnerabilities
Minimum citations: 4 findings
```

### [OT6] Web Server Misconfiguration Scan (nikto)
```
Action: Scan web server for common misconfigurations
Commands:
  nikto -h https://[target-url]
Analyze:
  - Server version disclosure
  - Dangerous HTTP methods enabled (PUT, DELETE, TRACE)
  - Default files and directories exposed
  - Backup files accessible (.bak, .old, .sql)
  - Debug endpoints exposed
Minimum citations: 3 findings
```

---

## 🔧 REMEDIATION WITHIN THIS PHASE

> ⚠️ **You MUST complete Rule OT-E (False Positive Triage) BEFORE fixing ANY finding.**
> Do NOT skip the triage. Do NOT fix findings without explicit user approval for EACH one.

After the user approves specific findings for fixing (via Rule OT-E triage), for each approved fix:
1. Show the tool output that identified the vulnerability
2. Apply the fix
3. Re-run the specific tool to verify the fix worked
4. Apply Rule OT-C (Hacker Mindset) to verify the fix doesn't create new problems
5. Document before/after results

---

## ⚠️ TOOL UNAVAILABILITY PROTOCOL

If a tool genuinely cannot be installed (e.g., no Docker, restricted environment):
1. **Document exactly what you tried** and the error message
2. **Perform manual equivalent checks** using curl, grep, and browser DevTools
3. **Mark the check as PARTIAL** in the gate report
4. **Never mark as PASS** if the tool couldn't run — mark as MANUAL_CHECK

---

## 📊 PHASE 13 GATE REPORT

```
╔══════════════════════════════════════════════════════════════╗
║  PHASE 13 GATE — Automated Offensive Testing               ║
╠══════════════════════════════════════════════════════════════╣
║ [OT1] ZAP Baseline:          [PASS/FAIL/PARTIAL]           ║
║ [OT2] Nuclei Scan:           [PASS/FAIL/PARTIAL]           ║
║ [OT3] SSL/TLS Testing:       [PASS/FAIL/PARTIAL]           ║
║ [OT4] Security Headers:      [PASS/FAIL/PARTIAL]           ║
║ [OT5] Dependency Vulns:      [PASS/FAIL/PARTIAL]           ║
║ [OT6] nikto Scan:            [PASS/FAIL/PARTIAL]           ║
╠══════════════════════════════════════════════════════════════╣
║ Tools Successfully Run:      [N/6]                          ║
║ Critical Findings:           [N]                            ║
║ Findings Fixed:              [N]                            ║
║ Remaining Risks:             [N]                            ║
╠══════════════════════════════════════════════════════════════╣
║ VERDICT: [PROCEED TO PHASE 14 / BLOCK — FIX FIRST]        ║
╚══════════════════════════════════════════════════════════════╝
```

> ⛔ **STOP — Do NOT proceed to Phase 14 until the user confirms.**

---

## 📌 MINIMUM CITATION REQUIREMENTS

| Check | Minimum Citations |
|-------|-------------------|
| OT1 - ZAP | 8 |
| OT2 - Nuclei | 5 |
| OT3 - SSL/TLS | 4 |
| OT4 - Headers | 4 |
| OT5 - Dependencies | 4 |
| OT6 - nikto | 3 |
| **Total** | **28** |

> Every citation MUST include: tool name, exact output snippet, URL/endpoint affected, and severity.
