# Provenance and source pins

Review date: 2026-11-12. Repository snapshots were fetched and checked out at the listed commits. No upstream installer or validation script was executed.

| Source | Commit | License | Selection / adaptation |
|---|---|---|---|
| <https://github.com/harshdhamaniya/mobile-security-skill> | `9edac3bd0a8a337cfc8b77fc42e046b7961b1390` | MIT | Adapted as project-local static-only mobile review; upstream Claude/SDK subagent and dynamic exploitation workflow excluded. |
| <https://github.com/ivan-magda/swift-security-skill> | `bda2e0ccee6a64d45ec2b93790d0876c90e4eb89` | MIT | Installed the skill and its reference documents unchanged. Review source freshness and deployment-target compatibility before relying on recommendations. |
| <https://github.com/UnitOneAI/SecuritySkills> | `70bc259bb01abb3015ad2ad859ad5253cbf0bcab` | MIT | Installed the selected appsec, identity, DevSecOps, and PCI review skills with relevant reference files. Re-linked shared local documentation and added a PCI DSS v4.0/v4.0.1 verification gate. Did not copy or execute repository validation scripts. |
| <https://github.com/dweinstein/mobile-security-skills> | `cb7ce51801057a52a91e883c80ce28f33bba73af` | No SPDX/license detected by GitHub API; no root `LICENSE` in the tree checked | Excluded. No skills or code copied. Reconsider only after rights are clarified. |

The first repository's README describes a Claude Code plugin with 18 agents and optional reverse-engineering tools. Its bundled workflow is not copied as an executable pipeline. The selected skills are instructions only; project-local governance constrains their use to static, read-only work.

The target repository itself has an EULA in `LICENSE`; its rights are separate from the MIT licenses on the selected skills. A source-visible or skill installation does not grant rights to modify, distribute, or commercially deploy the IOSSecuritySuite code.

## Activity observations

- Mobile source latest commit: 2026-10-08.
- Swift source latest commit: 2026-06-17 (repository metadata reported an update on 2026-10-23).
- SecuritySkills source latest commit: 2026-06-18 (repository metadata reported an update on 2026-11-11).
- Optional MASTG source latest commit: 2026-03-11; excluded for license uncertainty.

Pins are immutable commit identifiers; re-review before updating any pin.
