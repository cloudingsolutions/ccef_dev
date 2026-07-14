# Use Case

- Use Case ID: UC-CCEF-001
- Title: User creates an account with compliant onboarding defaults
- Product Slice ID: PS-CCEF-001
- Lifecycle State: Approved

## Summary
A new user registers for the cloud cost estimator, completes initial account setup, and receives an onboarding configuration that determines or confirms a supported data residency region and selected default language without silently assigning unsupported or indeterminate residency to an arbitrary region.

## Actor
New registered user

## Trigger
The user wants to start using the cloud cost estimator for the first time.

## Outcome
The user either has an authenticated account with a supported initial data residency region and selected default language, or reaches a clear designed stop state when residency is unsupported or indeterminate and cannot be assigned safely.

## Success Criteria
- The user can create an account and sign in after registration when onboarding reaches a supported residency outcome.
- During onboarding, the product determines an initial data residency outcome using available signals such as IP address and/or phone number where those signals are available and appropriate.
- Europe is supported as a minimum initial data residency region for the initial release.
- Where applicable regulation permits user choice, the user can select from supported data residency regions during onboarding.
- If residency is unsupported or cannot be determined with enough confidence under the approved residency decision policy, the product does not silently assign the user to an arbitrary region and instead presents a clear unsupported or indeterminate residency outcome as a designed stop state.
- Unsupported or indeterminate residency guidance explains what happened, whether the user can retry/correct inputs/contact support, and what cannot proceed until a supported residency outcome exists.
- The user can select a supported default language during onboarding, with English and Swedish supported in the initial release.

## Explicit Exclusions
- Team or organization role management beyond basic registered-user access
- Support for privacy/compliance regimes beyond the initial GDPR baseline unless separately defined
- Arbitrary residency assignment for unsupported or indeterminate users

## Linked Requirement IDs
- FR-CCEF-001
- FR-CCEF-002  (User sign-in and basic account management)
- FR-CCEF-010  (User dashboard and home experience)
- FR-CCEF-011  (Provider connection management)
- FR-CCEF-012  (Forecast management capabilities)
- NFR-CCEF-013  (Observability and monitoring requirements)