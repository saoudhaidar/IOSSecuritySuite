# Installation and prior-work risk assessment

Review date: 2026-11-12

## Skill-stack risks

| Risk | Rating | Evidence / treatment |
|---|---|---|
| Third-party prompt instructions can be stale or malicious | Medium | Reviewed selected entrypoints and repository instructions; selected skills use read-oriented guidance and include anti-injection/no-exfiltration rules. Treat all as untrusted and pin commits. Skills do not enforce tool permissions; only the four custom agents are configured with `read`/`search`. |
| Upstream mobile audit uses Claude/SDK subagents and dynamic tooling | High if used unmodified | README requires agent/task subagents and lists optional Frida/Objection/reverse-engineering tools. Installed version is rewritten as static-only; no agents or tools from that pipeline were copied or run. |
| PCI requirement revision mismatch | Medium | Selected PCI skill describes v4.0; official PCI SSC library showed v4.0.1. Do not issue compliance mappings without checking the current official text and QSA/ISA guidance. |
| SAMA/NCA control mapping freshness and applicability | High / unresolved | Official SAMA page was reachable but its body was not readable in the available page fetch; NCA fetch failed. No version, control IDs, or applicability claims are embedded as verified facts. Request controlled official documents. |
| Optional MASTG repository licensing | High / unresolved | GitHub API reported no license and the checked tree had no root LICENSE. Excluded and not copied. |
| Target project's own licensing | High / legal review required | `LICENSE` is a plan-based EULA, not a permissive OSS license. Skill licenses do not grant rights to the target source. |
| Swift security skill deployment assumptions | Medium | Upstream skill describes iOS 13+ as its minimum baseline, while this package declares iOS 11 in `Package.swift`. Verify availability and deployment support before applying any referenced API recommendation. |

## Review of the prior same-session security-suite enhancement

This was a source review only. No production source files were changed in the skill-installation task.

| Observation | Evidence | Risk / next action |
|---|---|---|
| Successful `fork()` is not cleaned up | `IOSSecuritySuite/RuntimeEnvironmentDetector.swift`, lines 54-69 call `fork()` and add a finding for any nonnegative result, but neither the child branch nor parent branch terminates/reaps the child. | High-priority correctness issue on environments where process creation succeeds; it can leave an additional running process. Remove this side effect or implement a safe, tested lifecycle before using the detector. |
| Frequency and allow-list configuration are not enforced | `SecurityArchitecture.swift`, lines 100-118 exposes `evaluationWindow` and `allowList`; the generator at lines 160-185 does not read them. | The API suggests controls that do not exist. Implement caching/policy semantics with deterministic tests or remove the unused options before production claims. |
| Signal capability metadata is not used | `SecurityDetectionProvider.supportedSignals` is declared at lines 154-158 but not checked by the generator. | Validate provider findings against declared signals or remove the unused contract. |
| Findings are max-severity aggregated, not a weighted independent-signal score | `SecurityReport` lines 145-150 selects the maximum risk; generator lines 169-180 filters confidence but does not calculate corroboration. | Do not describe this as multi-signal risk scoring. Define and test aggregation semantics before policy use. |
| Local policy is not server enforcement | `SecurityPolicyEvaluator` lines 188-203 returns a local action; no backend trust flow is implemented in this library. | High-value transaction authorization and fraud policy must remain server-enforced. |
| New detectors overlap on known paths and remain artifact heuristics | The rootless, Dopamine, and filesystem detectors inspect repeated fixed paths; the runtime detector checks library-name substrings and one Objective-C class. | Evidence can be hidden or spoofed and can create false positives. Keep as non-definitive indicators; add independent behavior/integrity evidence and device/server tests in a separate implementation task. |
| No regression test target was observed in the initial Xcode target list | `xcodebuild -list -project IOSSecuritySuite.xcodeproj -json` listed framework and sample app targets only. | Add focused tests for provider filtering, empty configuration, risk policy, fork handling, and detector evidence before production use. |

These are engineering review observations, not proof of a real-world bypass in a particular banking app or device.

## Recommended next tasks

1. In a separate production-code task, remove or safely contain the successful-fork side effect and add a focused regression test.
2. Define report evaluation-window, allow-list, provider-signal, and aggregation semantics; add deterministic tests before treating the policy API as a risk engine.
3. Validate jailbreak/runtime findings on supported device and simulator configurations with an approved test plan; do not treat path checks as a trust boundary.
4. Obtain current, authoritative SAMA and applicable NCA documents from the organization, confirm entity scope, and only then build a cited control mapping.
5. Review the banking app and backend separately for Keychain, TLS/pinning, App Attest, API authorization, transaction signing, device registration, and fraud-control implementation.
6. Confirm the skills and agents in a fresh VS Code Copilot session and perform the four smoke-review tasks there.
