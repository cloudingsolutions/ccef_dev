# Requirement

- Requirement ID: FR-CCEF-021
- Title: Phone Number Management in Account Settings
- Requirement Type: functional
- Product Slice IDs: PS-CCEF-001
- Lifecycle State: Approved

## Requirement Statement
The system shall allow users to view, update, and remove their verified phone number in account settings with appropriate consent handling.

## Rationale
Users need ongoing control over their phone number associated with their account for security, privacy, and preference reasons. Providing phone number management in account settings empowers users to maintain accurate contact information, update numbers when needed, and remove numbers when they no longer wish to receive SMS alerts, all while maintaining proper consent management.

## Acceptance Criteria
- Given a user has a verified phone number associated with their account
- When the user navigates to phone number settings in account management
- Then the system shall display the verified phone number (masked for privacy, showing last 4 digits)
- And the system shall indicate the verification status of the phone number
- And the system shall display the current SMS consent status
- And the system shall allow users to initiate a phone number update process
- And the system shall require re-verification for any new phone number (following FR-CCEF-018 and FR-CCEF-019)
- And the system shall handle consent appropriately when updating phone numbers (requiring fresh consent)
- And the system shall allow users to remove their phone number from their account
- And the system shall require explicit confirmation before removing a phone number
- And the system shall automatically withdraw SMS consent when a phone number is removed
- And the system shall clear associated verification and consent data when a phone number is removed
- And the system shall provide clear feedback on phone number update or removal success
- And the system shall prevent phone number removal if it would violate security policies (e.g., last 2FA method)
- And the system shall log all phone number management actions for audit purposes
- And the system shall enforce rate limiting on phone number change attempts to prevent abuse
- And the system shall handle edge cases gracefully (network failures, etc.)

## Explicit Exclusions
- Automatic phone number updates without user initiation
- Phone number sharing between accounts or family plans
- International phone number restrictions based on service availability
- Carrier-specific phone number features or services
- Temporary or disposable phone number usage
- Bulk phone number management operations

## Constraints
- Must require re-verification for any new phone number (full verification flow)
- Must withdraw existing SMS consent when phone number is changed or removed
- Must require fresh consent for any new or updated phone number
- Must mask phone numbers in UI displays for privacy (showing only last 4 digits)
- Must log all phone number management actions for audit and security purposes
- Must implement rate limiting on phone number change attempts
- Must not allow phone number removal if it compromises account security (e.g., only 2FA method)
- Must provide clear confirmation and feedback for all phone number actions
- Must handle phone number validation errors gracefully with user-friendly messages
- Must maintain backward compatibility with existing verified phone numbers
- Must comply with GDPR data subject rights regarding phone number data

## Validation Method
- Automated test: Unit tests for phone number management logic
- Automated test: Integration tests for phone number update and removal flows
- Manual QA: Testing phone number management in various account scenarios
- Security review: Validation of phone number data handling and security
- Architecture review: Confirmation of proper data flow and state management
- Compliance review: Validation of GDPR compliance in phone number management

## References
Approved artifacts this requirement should be interpreted with.

- Related Requirements, non-blocking:
  - FR-CCEF-018 (Phone Number Input and Validation for Verification)
  - FR-CCEF-019 (SMS Verification Code Generation and Validation)
  - FR-CCEF-020 (SMS Consent Capture and Recording)
- ADRs:
  - ADR-0001 (Modular Monolith with Clear Boundaries Approach)
- API / Data Contracts:
  - E.164 International Telecommunications Numbering Plan standard
  - GDPR-compliant data management specifications
- Policies / Regulations:
  - GDPR Article 16 (Right to rectification)
  - GDPR Article 17 (Right to erasure/'right to be forgotten')
  - GDPR Article 20 (Right to data portability)
  - TCPA (Telephone Consumer Protection Act)
- Design Artifacts:
  - ccef-ui-ux/prototype/index.html (phone number management implementation)
- Other:
  - NIST Special Publication 800-63B (Digital Identity Guidelines)
  - OWASP Authentication Security Guidelines
  - ISO 27001 (Information Security Management)

## Traceability
Planning objects this requirement supports or constrains.

- Product Slices:
  - PS-CCEF-001
- Use Cases:
  - UC-CCEF-004

Traceability rules:
- Every Requirement not marked Out of Scope must trace to at least one Product Slice.
- Every functional Requirement not marked Out of Scope must trace to at least one Use Case not marked Out of Scope or approved Product Slice objective.
- Every Use Case not marked Out of Scope must be covered by one or more functional Requirements not marked Out of Scope before implementation begins.
- Cross-cutting Requirements not marked Out of Scope may trace directly to the Product Slice when Use Case linkage would be artificial.
- Out of Scope Use Cases and Requirements are excluded from active traceability, coverage, and consistency checks. Links to or from Out of Scope artifacts may remain as historical/contextual references, but must not satisfy active implementation gates.
- Implementation work not covered by an approved Requirement is speculative and should be surfaced as a planning gap or marked as over-engineering.