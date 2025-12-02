# Scanner Comparison

## Only CodeQL (SAST) Found
- Flask app running in debug mode (High severity)
- Code-level misconfigurations that do not appear in HTTP responses
- Issues visible only through static code analysis

## Only ZAP (DAST) Found
- Missing security headers (CSP, X-Content-Type-Options, X-Frame-Options, Permissions-Policy)
- Runtime configuration issues (HTTP-only site, server info leakage)
- Live endpoint vulnerabilities visible only when the app is running
- Spectre isolation header issues (Cross-Origin-Resource-Policy)

## Only Dependency-Check (SCA) Found
- None, because 0 dependencies were detected in the scan

## All Three Tools
- (None — each tool analyzes a different layer: source code, runtime behavior, or dependencies)