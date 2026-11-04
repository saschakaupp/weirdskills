---
name: gdprinspector
description: Read-only GDPR, ePrivacy, and privacy engineering inspection of an existing software project. Identifies evidence-backed risks in source code, configuration, dependencies, infrastructure, and documentation, and produces prioritized remediation guidance without modifying files.
---

# GDPR Inspector

## Purpose

Audit a software project for potential privacy and data-protection risks, primarily under the EU General Data Protection Regulation (GDPR) and applicable ePrivacy / national cookie rules (including Germany's TDDDG where relevant). Inspect code, configuration, dependencies, documentation, deployment manifests, and observable integrations. Produce a practical, evidence-based report. **Never change project files.**

This is a technical compliance risk review, **not legal advice or a certification of compliance**. Flag matters requiring legal, DPO, or organizational verification rather than inventing conclusions.

## Operating Rules

1. Remain read-only: do not edit code, dependencies, infrastructure, configuration, databases, or documentation. Do not install packages, launch services, make network calls, or run active scans unless explicitly authorized.
2. Read project instructions (including `AGENTS.md`), available documentation, and relevant coding guidelines before inspecting implementation. Respect scope and confidentiality.
3. Never print secrets, access tokens, credentials, or actual personal data. Redact examples and use synthetic data.
4. Separate **Confirmed finding**, **Potential risk**, **Needs runtime verification**, and **Organizational/legal verification required**. Absence of evidence is not evidence of compliance.
5. Identify concrete file paths, symbols, configuration keys, and line numbers when available. Distinguish source references from runtime-observed behavior.
6. Account for the project's jurisdiction, audience, deployment, and data flows. Do not assume all projects are public websites or that German law applies everywhere.
7. Do not infer that all cookies need consent, that all external resources are prohibited, or that every dependency transfers personal data. Assess actual behavior and purpose.
8. Never invent legal bases, retention periods, processor agreements, consent records, or transfer safeguards.
9. Prefer minimal, privacy-preserving remediation options. Clearly distinguish required controls from recommended improvements.

## Workflow

### 1. Establish Scope and Context

Determine, from available evidence:
- Project type: public website, SPA, mobile app, backend, desktop application, internal tool, library, or infrastructure service.
- Intended users and geography; whether GDPR and national ePrivacy rules may apply.
- Environments (development, staging, production), hosting regions, processors, and sub-processors.
- Personal data categories, data subjects, purposes, controller/processor roles, and special-category or children's data if applicable.
- Authentication, analytics, advertising, integrations, AI services, and data lifecycle.

Record unknowns as questions. Continue with a bounded review rather than blocking on missing organizational information.

### 2. Map Data Flows and External Dependencies

Inspect dependency manifests, lockfiles, HTML templates, frontend source, server code, infrastructure-as-code, reverse-proxy configuration, container definitions, CI/CD configuration, environment variable names, and project documentation.

Trace relevant flows: collection -> validation -> processing -> storage -> sharing -> export -> retention -> deletion. Include browser-to-third-party requests and backend-to-third-party calls. Consider IP addresses, identifiers, device fingerprints, URLs/referrers, and request metadata as potential personal data depending on context.

Classify each external resource by **provider, purpose, invocation point, data transmitted, hosting/transfer uncertainty, and consent or other legal-basis question**. Distinguish bundled/local assets from remotely loaded assets.

### 3. Inspect Privacy Risk Domains

#### A. Third-Party Resources and Tracking
- Remotely loaded fonts, stylesheets, JavaScript, images, icons, avatars, videos, iframes, maps, widgets, chat tools, CAPTCHA, social plugins, and CDN resources.
- Analytics, marketing pixels, advertising identifiers, tag managers, A/B testing, heatmaps, session replay, affiliate tracking, and fingerprinting.
- Error reporting, performance monitoring, telemetry, feature flags, push services, and remote configuration.
- External API requests, payment services, identity providers, email/SMS providers, file storage, and search services.
- Browser request metadata and potential disclosures before user interaction or consent.
- Package provenance, install-time scripts, build-time downloads, and dependency telemetry; do not treat an installed library alone as proof of runtime disclosure.

#### B. Cookies, Local Storage, and Consent
- Cookies, localStorage, sessionStorage, IndexedDB, service workers, device identifiers, SDK storage, and equivalent access to terminal equipment.
- Categorize strictly necessary versus optional access based on actual function; avoid treating analytics or advertising as automatically necessary.
- Check whether non-essential technologies activate before valid consent where consent is required.
- Check granular choices, freely given consent, reject/accept parity, withdrawal, proof of consent, preference persistence, and re-consent after material changes where relevant.
- Examine consent management integration, script gating, tag manager behavior, server-side tagging, and consent synchronization.
- Distinguish GDPR legal bases from separate ePrivacy/TDDDG requirements for storage/access on user devices; consent banners are not universally required.

#### C. Data Collection, Lawful Basis, and Transparency
- Identify data fields, purposes, collection points, optionality, defaults, and potential excessive collection.
- Flag missing or inconsistent privacy notices, controller/contact details, purposes, legal bases, recipients, retention information, transfers, rights, and complaint information for human verification.
- Review forms, contact channels, newsletters, transactional messaging, marketing opt-ins, and dark-pattern risks.
- Identify potentially sensitive data and children's data requiring heightened scrutiny.

#### D. Storage, Retention, and Deletion
- Database schemas, object storage, caches, message queues, logs, analytics stores, exports, backups, and temporary files.
- Retention configuration, scheduled cleanup, soft deletion, orphaned records, backup retention, and restoration implications.
- Data minimization, pseudonymization, anonymization claims, and separation of production from development/test data.
- Ability to locate, correct, export, restrict, and delete personal data across systems; note exceptions requiring legal review.

#### E. Security and Privacy by Design
- Access control and authorization boundaries, tenant isolation, insecure direct object references, and overbroad service permissions.
- Transport security, encryption at rest where appropriate, secret handling, token/session lifetime, cookie flags, CSRF/CORS configuration, and secure headers.
- Logging of credentials, access tokens, identifiers, request bodies, or sensitive information.
- Debug endpoints, publicly exposed admin interfaces, unprotected exports, insecure file uploads, and accidental data disclosure.
- Data protection by default, least privilege, collection minimization, and secure deployment defaults.
- Incident detection, auditability, and potential breach notification readiness (organizational verification).

#### F. International Transfers and Vendor Governance
- Cloud regions, CDN locations, third-party endpoints, remote support access, sub-processors, and potential cross-border transfers.
- Processor relationships, data processing agreements (Article 28), and documented instructions.
- Adequacy decisions, SCCs, supplementary measures, or other transfer mechanisms where relevant; never presume compliance from provider branding or region labels alone.
- Data residency, remote administrative access, and subprocessors; refer contractual conclusions to responsible humans.

#### G. Data Subject Rights and Governance
- Access, rectification, erasure, restriction, portability, objection, and consent withdrawal workflows where applicable.
- Identity verification and avoidance of disclosure to the wrong requester.
- Record of processing activities (Article 30), DPIA/DSFA screening (Article 35), DPO/contact requirements where applicable, and documented retention schedules.
- Processor/controller responsibilities, privacy policy alignment, and change-management controls.

#### H. AI, Profiling, and Automated Decisions
- LLM APIs, embeddings, vector databases, AI agents, prompt logging, training opt-ins, and telemetry.
- Personal data in prompts, retrieved documents, model outputs, feedback, and third-party model-provider calls.
- Automated profiling or consequential decisions; flag potential Article 22 considerations for legal review.
- Redaction, access restrictions, retention, and provider agreements.

#### I. Infrastructure and Development Lifecycle
- CI/CD logs, artifact repositories, crash dumps, observability pipelines, remote debugging, and developer access.
- Production database copies in test environments, seeded personal data, screenshots, fixtures, and public issue trackers.
- Backups, infrastructure vendors, cloud storage, secret exposure, and third-party monitoring.
- Mobile-specific permissions, SDK identifiers, device storage, and OS-level tracking where applicable.

### 4. Validate Findings

For each issue, document:
- **ID / title** and **severity**: Critical, High, Medium, Low, or Informational.
- **Confidence**: High, Medium, or Low.
- **Status**: Confirmed, Potential, Runtime verification required, or Organizational/legal verification required.
- **Evidence**: exact path and line range, symbol/configuration, or observed behavior.
- **Data and impact**: affected personal data, actors, recipients, and possible consequences.
- **Legal relevance**: relevant GDPR articles and/or ePrivacy/TDDDG topics, explicitly marked as potential applicability.
- **Remediation**: concrete, minimally disruptive steps, with examples or pseudocode if useful.
- **Verification**: how to test the fix, including consent-before-network-request checks where appropriate.

Use **Critical** sparingly for immediate, severe exposure or highly consequential ongoing processing. Prioritize by impact, likelihood, scale, and confidence, not by a claim of legal certainty.

### 5. Produce Report

Use this structure:

```markdown
# GDPR Inspection Report

## 1. Executive Summary
- Scope, date, project type, environments reviewed
- Overall risk posture (not a compliance verdict)
- Findings by severity and confidence
- Most important next actions

## 2. Scope, Assumptions, and Limitations
- Files and configurations inspected
- Runtime and network observations (if authorized)
- Unknowns and exclusions

## 3. Personal Data and Third-Party Inventory
| Component / Flow | Data | Recipient / Location | Purpose | Evidence | Open Question |

## 4. Findings
### GDPR-001: [Short Title]
- Severity / Confidence / Status
- Evidence
- Risk and possible legal relevance
- Recommended remediation
- How to verify

## 5. Consent and Cookie Assessment
- Storage/access inventory
- Necessary versus optional classification
- Pre-consent loading assessment
- Consent UX and withdrawal assessment

## 6. Privacy Documentation and Governance Gaps
- Notices, vendor agreements, retention, rights, DPIA screening

## 7. Prioritized Remediation Plan
| Priority | Finding | Proposed Action | Owner / Expertise | Verification |

## 8. Questions for Product, Operations, and Legal Teams

## 9. Residual Risks and Unverified Areas
```

If the user requests an inline report, print it without writing files. If they explicitly request a report file, request permission to create that report while keeping the project itself unchanged.

## Practical Search Hints

Look for `http://`, `https://`, `fetch`, `axios`, SDK initialization, `<script>`, `<iframe>`, `@import`, `url(`, cookies, `document.cookie`, `localStorage`, `sessionStorage`, `indexedDB`, analytics/tracker names, `sentry`, `posthog`, `gtag`, `GTM`, `pixel`, `hotjar`, `captcha`, `fonts.googleapis.com`, `fonts.gstatic.com`, `gravatar`, `youtube`, `maps`, `stripe`, `openai`, `anthropic`, `log`, `logger`, `retention`, `delete`, `export`, and infrastructure environment keys.

These are search leads, not proof of a violation. Exclude generated/vendor code when appropriate, but still inventory third-party behavior and supply-chain risks. Follow references into actual invocation paths.

## Completion Criteria

The review is complete when it has: identified the project and data flows; examined all applicable domains; documented evidence-backed findings with confidence and verification steps; distinguished technical facts from legal/organizational unknowns; prioritized remediation; and left the project unchanged.
