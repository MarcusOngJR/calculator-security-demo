# Security Scanning

## Overview
This repository uses three types of security scanning:

## SAST (Static Analysis with CodeQL)

### What it does
- Analyzes source code without executing it
- Detects vulnerabilities such as:
  - Logic flaws
  - Unsafe code patterns
  - Dangerous API usage
  - Misconfigurations (e.g., Flask debug mode)

### When it runs
- On every push and pull request to **main** or **master**

### What it checks for
- Code-level vulnerabilities
- Data flow issues
- Hardcoded secrets (if enabled)
- Framework-level misconfigurations

### Artifacts
- View results in **GitHub → Security → Code Scanning Alerts**
- SARIF output (if uploaded) available in workflow artifacts

---

## SCA (Dependency Check)

### What it does
- Scans third-party packages for known CVEs
- Uses multiple vulnerability databases:
  - NVD
  - OSS Index
  - CISA KEV
  - RetireJS

### When it runs
- On every push and pull request to **main** or **master**

### What it checks for
- Outdated package versions
- Known CVEs in dependencies
- Deprecated/retired libraries
- CVSS severity scoring

### Artifacts
- Reports stored in workflow artifacts under:
  - **`sca-reports/`**
- Formats include:
  - HTML
  - JSON
  - XML
  - CSV

> Note: Currently showing 0 dependencies because Python `site-packages` path must be scanned instead of `.`.

---

## DAST (Live Application with ZAP)

### What it does
- Starts the application and performs active runtime scanning
- Detects vulnerabilities visible in HTTP responses, such as:
  - Missing security headers
  - Protocol configuration issues
  - Runtime misconfigurations
  - Server information leakage
  - Insecure endpoint behavior

### When it runs
- After the application builds successfully
- On every push and pull request to **main** or **master**

### What it checks for
- Missing headers:
  - Content-Security-Policy
  - X-Frame-Options
  - X-Content-Type-Options
  - Permissions-Policy
  - CORP (Spectre protection)
- HTTP/HTTPS configuration issues
- Server technology disclosure
- Basic spidering of accessible endpoints

### Artifacts
- Baseline scan: **`zap-baseline-reports/`**
- Full scan: **`zap-fullscan-reports/`**
- Includes:
  - HTML
  - Markdown
  - JSON reports

---

## Understanding Results
See **Part 10 in README** for interpretation, severity scoring, and triage workflow.

---

## Reporting Vulnerabilities
If you discover or suspect a security issue:

📧 **Email:** `security@example.com`

Include:
- Description of the issue
- Steps to reproduce
- Logs or screenshots
- Estimated severity (optional)