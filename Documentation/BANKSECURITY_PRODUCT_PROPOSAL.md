# WIP: Proposal for a separate BankSecurity product

**Status:** Discussion draft only. Awaiting written confirmation from SecuRing and legal review.

This document proposes evaluating a separate product named **BankSecurity** for banking-focused iOS security capabilities. It does not rename IOSSecuritySuite, grant permission to modify or redistribute it, or authorize implementation of the proposed product.

## Context

The repository's `LICENSE` is a plan-based EULA. Section III.2 asks users to contact SecuRing before developing the software with a correction, supplement, or patch. The README also describes commercial licensing for modules that use IOSSecuritySuite. The applicable permissions and license plan for the proposed product have not been confirmed.

Accordingly, this PR contains no IOSSecuritySuite source changes and does not include or rebrand the pending local source modifications.

## Proposal

Evaluate BankSecurity as a distinct package/product with its own name, API, documentation, release process, and tests. Do not rename or present IOSSecuritySuite as BankSecurity.

Before choosing an implementation model, obtain written answers from SecuRing and legal review for at least these questions:

- May BankSecurity depend on IOSSecuritySuite, and under what license plan and distribution conditions?
- May BankSecurity include, adapt, or distribute any IOSSecuritySuite source or binaries?
- What attribution, notices, branding, and source-provenance requirements apply?
- May proposed fixes or extensions be developed and submitted upstream?

Subject to those answers, assess these alternatives:

1. **Separate integration layer:** BankSecurity uses IOSSecuritySuite only through an approved dependency and keeps its banking-specific API and policy separate. Confirm that the EULA permits this product and its distribution before implementation.
2. **Independent implementation:** BankSecurity is implemented from independently authored code and requirements without copying or modifying IOSSecuritySuite. Obtain legal review of provenance, compatibility, and any use of project names or marks.

Neither alternative should be treated as approved merely because this proposal is accepted or merged.

## Product principles

- Keep device-side detections as risk signals, not authorization decisions.
- Require server-side enforcement for account access and high-value actions.
- Make signal provenance, confidence, and limitations explicit to integrators.
- Minimize collection and retention of device and user data.
- Verify platform/API availability against the supported iOS range.
- Add regression tests for security behavior and document bypass and false-positive limitations.

## Approval and implementation gates

Implementation should not begin until the project owner records written licensor confirmation and legal review of the proposed product, license plan, and distribution model. After approval:

1. Record the approved product and dependency boundaries, license notices, and attribution.
2. Select and document the package/module structure and supported iOS/Swift versions.
3. Review the existing proposed detector and reporting changes independently; do not assume they are accepted upstream or licensed for reuse.
4. Address the reported process-fork control-flow issue and add regression coverage before considering that behavior production-ready.
5. Validate package, Xcode, and supported integration workflows, then review the resulting changes before release.

## Decision requested

This WIP PR requests feedback on whether to pursue a separate BankSecurity product and asks for the written licensing and modification guidance needed to choose a lawful implementation path. It is not a request to merge or publish code derived from IOSSecuritySuite.
