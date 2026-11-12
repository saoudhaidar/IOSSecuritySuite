---
name: banking-ios-security-governance
description: Review iOS banking security and governance concerns including account takeover, device binding, authentication, transaction authorization, replay resistance, API authorization, fraud signals, App Attest, sensitive data, audit logging, SAMA/NCA applicability, and PCI DSS scope.
---

# Banking iOS security governance

Use for design, implementation, or review of banking and fintech security changes. This skill provides review questions; it does not certify regulatory compliance or make a local device a trust authority.

## Review domains

- **Account takeover:** trace enrollment, login, recovery, step-up, credential reset, session refresh, logout, revocation, and suspicious-activity handling. Check server-side rate limits, credential stuffing controls, recovery assurance, and risk-based step-up.
- **Device binding and registration:** verify registration is authenticated, cryptographically bound to a device-held key, protected against replay, revocable, auditable, and recoverable after device replacement. Do not treat an identifier, jailbreak result, or client-provided device claim as proof of identity.
- **Authentication and sessions:** inspect token issuance, audience/scope, expiry, refresh rotation, revocation, concurrency, secure Keychain storage, and redaction. Avoid fail-open behavior on ambiguous biometric or network outcomes.
- **Biometric authorization:** use biometrics as a local authorization factor bound to protected key material where supported; do not treat an `LAContext` boolean as a substitute for server authorization or transaction binding.
- **Transaction authorization:** bind authorization to the exact transaction details (including amount, currency, recipient, and relevant changeable fields); require server-side verification, clear user confirmation, and step-up when policy requires it.
- **Anti-replay:** validate nonces/challenges, expiry, uniqueness, request binding, idempotency, and server-side replay rejection. Do not rely on client timestamps alone.
- **API authorization:** verify server-side object- and function-level authorization on every request, including ownership/tenant boundaries, transaction limits, idempotency, and state transitions. Treat client role, account, and risk claims as untrusted.
- **Fraud and risk signals:** document signal source, freshness, confidence, privacy impact, spoofability, and server-side decision ownership. A single local signal must not be a definitive fraud decision.
- **App Attest:** where available and applicable, verify the server challenge, attestation/assertion, app identity, key lifecycle, counter/replay semantics, and failure policy on the server. Check Apple’s current documentation and OS availability before implementation. App Attest is a signal, not a substitute for authorization.
- **Sensitive data:** classify data; minimize collection and retention; protect secrets with appropriate Keychain access controls; prevent secrets, authentication factors, PAN, and personal/financial data from entering logs, crash reports, analytics, screenshots, or backups without a documented basis.
- **Audit logging:** record security-relevant events with actor, action, result, correlation, and trusted server time where available. Redact secrets and minimize personal data; define integrity, access, retention, and deletion requirements from verified policy.

## Regulatory applicability and control mapping

1. Establish the legal entity, product, geography, data flows, cardholder-data scope, outsourcing model, and regulator before mapping controls.
2. For Saudi Central Bank-regulated entities, consult the current official SAMA Cyber Security Framework and organization-approved applicability/assessment material. The framework may be scoped differently by entity type; do not infer applicability from this repository.
3. For applicable NCA requirements, use the effective official NCA publication and confirm the organization is within its scope. Do not cite a control number, version, or mandatory status unless checked against that exact official source.
4. Apply PCI DSS only when cardholder data or the applicable connected/security-impacting environment is in scope. Determine scope first and verify every requirement against the current PCI SSC publication and the organization’s QSA/ISA direction.
5. Record the source title, issuer, version/date, exact control text, applicability rationale, evidence, and interpretation. If the official document is unavailable, state that the mapping is unverified and request the controlled document; do not fabricate references.

Sources to verify for the assessment in this repository:

- SAMA Cyber Security Framework page: <https://www.sama.gov.sa/en-US/Laws/BankingRules/Pages/CyberSecurityFramework.aspx>
- NCA official portal: <https://nca.gov.sa/>
- PCI SSC document library: <https://www.pcisecuritystandards.org/document_library/?category=pcidss&document=pci_dss>
- Apple App Attest documentation: <https://developer.apple.com/documentation/devicecheck>
- OWASP MASVS: <https://mas.owasp.org/MASVS/>
- OWASP MASTG: <https://mas.owasp.org/MASTG/>

The official PCI SSC document library was checked on 2026-11-12 and displayed PCI DSS v4.0.1. Do not rely on a vendored skill written for an earlier revision without checking the current official text.

## Output

Report confirmed evidence separately from assumptions. Include the business/data-flow scope, applicable control sources and versions, gaps, compensating controls if formally approved, test evidence, owner, and unresolved questions. Do not claim compliance or security effectiveness from a source review alone.
