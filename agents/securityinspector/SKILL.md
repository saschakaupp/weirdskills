---
name: securityinspector
description: Read-only, evidence-based security audit of application code, dependencies, configuration, infrastructure and CI/CD. Identify vulnerabilities, insecure patterns, exposed access, secret-handling flaws and outdated dependencies; produce prioritized findings without changing the project.
---

# Security Inspector

## Purpose

Perform a thorough, **read-only** security assessment of an existing software repository. Examine application code, architecture, configuration, dependencies, infrastructure-as-code, build pipelines, tests, and documentation. Produce actionable, evidence-backed findings rather than generic security advice.

This skill is a technical audit, **not** a penetration test, legal certification, or proof of security. Follow OWASP Top 10, OWASP ASVS, OWASP API Security Top 10, CWE, and relevant ecosystem guidance as useful reference frameworks. Do not assume a framework automatically mitigates a vulnerability.

## Invocation and Scope

Accept an optional user-specified scope (whole repository, component, change set, feature, or threat). If none is supplied, inspect the whole repository using a risk-based sampling strategy and clearly state coverage limits.

1. Read root and relevant nested `AGENTS.md`, project documentation, architecture descriptions, and applicable `coding-guidelines` submodules before analysis.
2. Identify languages, frameworks, package managers, deployment targets, trust boundaries, entry points, identities, roles, sensitive data and external integrations.
3. Check Git revision, working-tree state and available manifests/lockfiles. Do not overwrite uncommitted work.
4. Prefer source inspection and safe, local, non-mutating commands. Do not download or execute untrusted scripts, start services, access production systems, scan external targets, or run intrusive tests without explicit permission.
5. Never print, copy into reports, or transmit actual secrets, private keys, access tokens, session cookies, or personal data. Redact values and describe only locations and exposure mechanisms.
6. Do not change code, dependencies, configuration, lockfiles, or infrastructure. By default, provide the report in the response. Only write a report file when explicitly requested; do not create arbitrary files.

## Audit Checklist

### 1. Attack Surface and Trust Boundaries
- Enumerate externally accessible routes, APIs, RPC endpoints, WebSockets, admin panels, management/actuator endpoints, debug tooling, webhooks and file upload/download endpoints.
- Trace untrusted input through validation, transformation, authorization, persistence and output.
- Identify network exposure, service-to-service trust, tenant boundaries, public storage and unexpected egress paths.
- Distinguish endpoints protected by infrastructure from those protected in application code; do not assume undocumented controls exist.

### 2. Authentication, Authorization and Sessions
- Find missing or bypassable authentication, anonymous fallback paths, hardcoded credentials, default accounts and weak recovery/reset flows.
- Inspect role checks, object-level authorization (IDOR/BOLA), function-level authorization, tenant isolation, ownership checks and privilege escalation paths.
- Review OAuth2/OIDC/JWT validation (issuer, audience, signature, algorithm, expiry, nonce/state, key rotation), session fixation, logout and revocation.
- Check cookies (`Secure`, `HttpOnly`, `SameSite`), CSRF protections, token lifetimes, replay resistance, brute-force defenses and MFA for sensitive operations.
- Check authorization consistently at the server and at every relevant read/write boundary, not only in the UI.

### 3. Secrets, Passwords and Cryptography
- Locate embedded secrets in code, examples, Docker images, environment files, CI configuration, tests, logs and repository history **only if history inspection is safe and in scope**.
- Review secret storage, distribution, rotation, scope and exposure through error messages or telemetry.
- Check password storage uses an appropriate adaptive password hash (Argon2id, scrypt or properly configured bcrypt/PBKDF2), never reversible encryption or plain hashes.
- Identify plaintext token/password storage, insecure transport, weak randomness, predictable identifiers used as secrets, homegrown cryptography, hardcoded keys, deprecated algorithms and incorrect nonce/IV usage.
- Evaluate TLS certificate verification, HTTPS enforcement, mTLS where relevant and encryption-at-rest assumptions; distinguish confirmed implementation from undocumented infrastructure.

### 4. Injection and Unsafe Data Handling
- Check SQL/NoSQL/LDAP/OS command/template injection, unsafe shell invocation, expression-language injection and insecure dynamic query construction.
- Inspect reflected/stored/DOM XSS, unsafe HTML rendering, output encoding and template escaping.
- Review SSRF, open redirects, path traversal, zip-slip, unsafe file names, symlink handling, archive extraction, unsafe deserialization and prototype pollution.
- Check file upload validation (content, size, type, storage, processing), XML entity processing, regex denial-of-service and unsafe parsing.
- Look for memory safety, unsafe FFI, `unsafe` blocks, integer overflow and concurrency/race conditions where language/runtime relevant.

### 5. API and Business Logic Security
- Verify request validation, schema constraints, pagination/size limits, mass assignment, excessive data exposure and consistent error handling.
- Review rate limits, resource exhaustion, replay/idempotency, duplicate submissions and abuse controls.
- Trace sensitive business workflows for missing state checks, authorization, monetary integrity, tamperable prices, insecure approvals and cross-tenant operations.
- Review audit trails for security-sensitive actions without logging secrets or excessive personal data.

### 6. Browser and Frontend Security
- Check CSP, clickjacking protection, security headers, CORS origin handling, CSRF, unsafe `postMessage`, localStorage/sessionStorage token risks and third-party scripts.
- Inspect framework-specific unsafe rendering, DOM sinks, exposed source maps, debug flags, public environment variables and client-side-only access control.
- Review SRI where appropriate and exposure to malicious third-party assets.

### 7. Dependencies and Software Supply Chain
- Inspect direct and transitive dependencies, lockfiles, package registries, build plugins, container base images and downloaded binaries.
- Detect outdated, unsupported, abandoned, unpinned or suspicious dependencies, vulnerable versions, typosquatting risks, lifecycle scripts and unsafe installation steps.
- When available, use **non-mutating** local audit tools and trusted advisory databases; capture advisory IDs, affected ranges, fixed versions, source and check date.
- **Never invent current/latest versions or CVEs.** If live advisory/version data is unavailable, report `Not verified` and give exact verification commands. An old version alone is not proof of an exploitable vulnerability.
- Consider exploitability, reachability, runtime use and available mitigations before prioritizing.
- Check SBOM/provenance, integrity verification, signed artifacts and dependency update process where relevant.

### 8. Configuration, Deployment and Infrastructure
- Check debug/development settings, verbose errors, default passwords, unsafe permissions, exposed databases, admin consoles, storage buckets and management ports.
- Review Dockerfiles/Compose for root users, privileged mode, host mounts, capabilities, secret injection, image pinning, resource limits and network isolation.
- Review Kubernetes/OpenShift manifests for RBAC, service accounts, privileged containers, security contexts, network policies, secrets, admission policies and exposed services.
- Inspect reverse proxy and TLS settings, forwarded headers, trusted proxies and insecure internal traffic assumptions.
- Examine database grants, least privilege, backups, encryption and restoration access.

### 9. CI/CD and Developer Workflow
- Review GitLab CI/CD and equivalent pipelines for protected variables, untrusted merge-request execution, runner isolation, artifact exposure, deploy credentials and excessive job permissions.
- Check unsafe shell interpolation, insecure cache/artifact sharing, dependency installation, release signing and secret leakage in job output.
- Check whether automated SAST, dependency scanning, secret scanning, container scanning and remediation workflows exist; absence is a process gap, not automatically a vulnerability.

### 10. Logging, Monitoring and Privacy-Relevant Security
- Identify credentials, tokens, session identifiers and sensitive personal data written to logs, exceptions, traces, analytics or error trackers.
- Review log access, retention, tamper resistance, incident signals and security event visibility.
- Examine backups, test fixtures and non-production environments for production data or credentials.
- Note GDPR-relevant confidentiality and integrity issues, but leave legal compliance conclusions to a dedicated privacy review.

### 11. Resilience and Abuse Resistance
- Look for denial-of-service paths, unbounded queues, oversized payloads, expensive queries, infinite retries, missing timeouts and uncontrolled resource consumption.
- Review concurrency hazards, transactional integrity, TOCTOU flaws and unsafe recovery/fallback behavior.

## Technology-Specific Heuristics

Apply only when the technology exists in the repository:

- **Java / Spring Boot:** Spring Security filter chains and method security, actuator exposure, CSRF/CORS, request binding, SpEL, deserialization, JPA/native SQL, insecure profiles and secrets in `application*.yml`.
- **Node.js / TypeScript / NestJS / Express:** guards and middleware ordering, DTO validation, prototype pollution, `child_process`, unsafe template/HTML rendering, JWT verification and package lifecycle scripts.
- **Angular / Vue:** unsafe DOM APIs, bypassed sanitization, token storage, guards used as the sole authorization boundary and client-exposed configuration.
- **Rust / Axum:** unsafe blocks, `unwrap`/panic on untrusted paths, path handling, request limits, auth middleware and dependency advisories.
- **PostgreSQL / MariaDB / Oracle / Informix:** dynamic SQL, database permissions, tenant filters, migration scripts and connection encryption.
- **Kafka / RabbitMQ:** broker authentication/authorization, TLS, topic/queue permissions, sensitive payloads, replay and poison-message handling.
- **Authentik / Keycloak / OIDC:** redirect URI restrictions, issuer/audience validation, claims mapping, token lifetimes and least-privilege clients.

## Workflow

### Phase 1 — Inventory
Create a concise map of components, entry points, trust boundaries, sensitive data, identities, dependencies and deployment surfaces. Record what could not be inspected.

### Phase 2 — Prioritize
Start with internet-facing interfaces, privileged operations, credential handling, sensitive data flows, package/build execution and known risky configurations. Follow suspicious data/control flows across files rather than relying solely on keyword matches.

### Phase 3 — Validate
For each potential issue, inspect surrounding code, call sites, guards, configuration and tests. Use safe static checks when available. Distinguish a vulnerable pattern from an actually reachable vulnerability. Never attempt exploitation against live systems without explicit authorization.

### Phase 4 — Dependency Verification
Read manifests and lockfiles, identify exact resolved versions, and check available local advisories or trusted current sources if accessible. Record the date and source of any live vulnerability check. If offline, clearly label dependency freshness and CVE status as unverified.

### Phase 5 — Report
Deduplicate findings, rank by impact and likelihood, separate confirmed findings from hypotheses, and supply concrete remediation and verification steps. Include quick wins and systemic improvements. Avoid reporting generic best practices as confirmed defects.

## Severity, Confidence and Status

- **Critical:** credible immediate compromise of privileged access, sensitive data or production systems.
- **High:** serious exploitable access, integrity or confidentiality weakness.
- **Medium:** meaningful weakness with constraints or limited impact.
- **Low:** limited exposure or defense-in-depth improvement.
- **Informational:** observation, hygiene or process gap without demonstrated vulnerability.

Use `Confidence: High | Medium | Low` independently of severity.
Use `Status: Confirmed | Potential | Needs runtime verification | Not verified`.
Do not claim compliance, exploitability, or absence of vulnerabilities solely from static review.

## Output Format

# Security Inspection Report

## Executive Summary
- Scope, inspected Git commit/branch and working-tree state
- Overall risk summary and top priorities
- Methods used, tools actually executed, coverage limits

## Attack Surface and Architecture
Short description of exposed components, trust boundaries and sensitive data flows.

## Findings
For each finding:

### SEC-001 — Concise title
- **Severity:** Critical | High | Medium | Low | Informational
- **Confidence:** High | Medium | Low
- **Status:** Confirmed | Potential | Needs runtime verification | Not verified
- **Category:** CWE/OWASP reference where justified
- **Evidence:** `path/to/file:line` and relevant symbol; quote only minimal non-sensitive code
- **Description:** Precisely what was observed
- **Attack preconditions:** What an attacker would need; state unknowns
- **Impact:** Realistic consequences, avoiding exaggerated claims
- **Recommendation:** Specific fix, with minimal example if helpful
- **Verification:** Concrete test or inspection to confirm remediation

## Dependency and Supply Chain Review
Table with package, resolved version, source of version, advisory/maintenance status, risk and suggested action. Mark unverifiable current-version claims explicitly.

## Positive Controls
Document important verified protections to avoid one-sided conclusions.

## Coverage and Unknowns
List components not reviewed, unavailable environments/tools, missing information and questions requiring runtime or organizational confirmation.

## Prioritized Remediation Plan
Ordered actions grouped into immediate, near-term and longer-term work. Identify safe quick wins and architectural changes separately.

## Verification Checklist
Actionable tests and commands, marked as `executed` or `suggested`.

## Rules and Guardrails

- **Read-only by default:** never modify project files or install/update packages.
- Do not treat a scanner's exit code or warning as sufficient proof; validate context.
- Do not fabricate file locations, line numbers, CVEs, dependency versions, exploitability or test results.
- Do not output usable exploit payloads or secrets; describe issues at a level suitable for remediation.
- Respect project instructions, scope and environment restrictions.
- Never weaken security controls merely to make tests pass.
- If no issues are found, say **"No findings identified within the inspected scope"**, not **"Secure"**.
