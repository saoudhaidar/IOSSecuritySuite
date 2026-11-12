# Security skill installation inventory

Review date: 2026-11-12

## Agent environment

- Detected in this session: GitHub Copilot in VS Code (Copilot SDK).
- Workspace skill location: `.github/skills/`, per the current VS Code Agent Skills documentation.
- Workspace custom agents: `.github/agents/*.agent.md`, per VS Code custom-agent documentation.
- Project instructions: root `AGENTS.md`.
- The existing personal `~/.agents/skills/` links were inspected and left unchanged.

## Installed project-local skills

| Skill | Focus | Source |
|---|---|---|
| `mobile-security-audit` | Read-only iOS mobile review: jailbreak/runtime resilience, network trust, auth, storage, crypto, platform | Project adaptation; source and license in skill directory |
| `swift-security-expert` | Keychain, Secure Enclave, CryptoKit, biometrics, certificate trust | `ivan-magda/swift-security-skill` |
| `secure-code-review` | Secure source review | `UnitOneAI/SecuritySkills` |
| `threat-modeling` | STRIDE and threat modeling | `UnitOneAI/SecuritySkills` |
| `api-security` | API authorization and OWASP API Security Top 10 | `UnitOneAI/SecuritySkills` |
| `dependency-scanning` | Dependency and supply-chain review | `UnitOneAI/SecuritySkills` |
| `secrets-management` | Secrets handling and lifecycle | `UnitOneAI/SecuritySkills` |
| `iam-review` | IAM and access review | `UnitOneAI/SecuritySkills` |
| `pipeline-security` | CI/CD pipeline security | `UnitOneAI/SecuritySkills` |
| `pci-dss-review` | PCI DSS assessment aid; must be checked against current PCI SSC text | `UnitOneAI/SecuritySkills` |
| `banking-ios-security-governance` | Banking mobile governance and regulatory applicability | Project-authored |
| `security-skill-orchestrator` | Selective routing and progressive disclosure | Project-authored |

## Installed custom agents

- `Mobile Security Reviewer`
- `Swift Security Reviewer`
- `Banking API Security Reviewer`
- `Security Governance Reviewer`

All are configured as read-only `read`/`search` agents. Actual availability and invocation in the VS Code UI must be confirmed in a fresh Copilot session.
