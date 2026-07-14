Requirement ID: FR-CCEF-001
Title: User registration with compliant onboarding defaults
Requirement Type: functional
Product Slice IDs: PS-CCEF-001
Lifecycle State: Approved

# Requirement Statement
The system shall allow new users to register for an account, complete initial account setup, and receive an onboarding configuration that determines or confirms a supported data residency region and selected default language without silently assigning unsupported or indeterminate residency to an arbitrary region.

# Rationale
This requirement ensures compliant user onboarding that respects data residency regulations and provides clear outcomes when residency cannot be supported, preventing arbitrary assignment to regions that may violate compliance requirements.

# Acceptance Criteria
- Given a new user wants to start using the cloud cost estimator
- When the user completes registration and initial account setup
- Then the system shall determine an initial data residency outcome using available signals such as IP address and/or phone number where those signals are available and appropriate
- And Europe shall be supported as a minimum initial data residency region for the initial release
- And where applicable regulation permits user choice, the user shall be able to select from supported data residency regions during onboarding
- And if residency is unsupported or cannot be determined with enough confidence under the approved residency decision policy, the system shall not silently assign the user to an arbitrary region and shall instead present a clear unsupported or indeterminate residency outcome as a designed stop state with HTTP 409 Conflict status and error message indicating unsupported/indeterminate residency
- And unsupported or indeterminate residency guidance shall explain what happened, whether the user can retry/correct inputs/contact support, and what cannot proceed until a supported residency outcome exists
- And the user shall be able to select a supported default language during onboarding, with English and Swedish supported in the initial release returning HTTP 200 OK with selected language in response headers
- And the system shall return HTTP 201 Created for successful registration with user ID and session token in response body

# Explicit Exclusions
- Team or organization role management beyond basic registered-user access
- Support for privacy/compliance regimes beyond the initial GDPR baseline unless separately defined
- Arbitrary residency assignment for unsupported or indeterminate users

# Constraints
- The product must determine an initial data residency region during onboarding using available signals such as IP address and/or phone number
- Europe is the minimum supported residency region for the initial release
- Where applicable regulation permits user choice, the user may select another supported residency region during onboarding
- The product must not silently assign users with unsupported or indeterminate residency to an arbitrary region
- The initial release must meet GDPR as the minimum compliance baseline
- The product must support localization and user-selectable default language
- The initial release must support English and Swedish for all in-scope core user-facing copy and alert content
- For test harness implementation, allowed signal-source combinations are: (IP only), (phone only), (IP and phone), or (neither - results in indeterminate state)
- All HTTP endpoints must enforce TLS 1.2+ encryption for data in transit

# Validation Method
- automated test
- manual QA
- code review

# References
- Related Requirements, non-blocking:
- ADRs:
- API / Data Contracts:
- Policies / Regulations: GDPR
- Design Artifacts:
- Other:

# Traceability
- Product Slices: PS-CCEF-001
- Use Cases: UC-CCEF-001