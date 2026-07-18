# Requirement

- Requirement ID: FR-CCEF-019
- Title: SMS Verification Code Generation and Validation
- Requirement Type: functional
- Product Slice IDs: PS-CCEF-001
- Lifecycle State: Approved

## Requirement Statement
The system shall generate, send, and validate one-time verification codes via SMS for phone number verification.

## Rationale
SMS verification codes provide a secure method to confirm that the user has access to the phone number they provided. This two-factor authentication step ensures that phone numbers cannot be fraudulently added to accounts, enhancing security and preventing abuse of the SMS alert system.

## Acceptance Criteria
- Given a user has entered and validated a phone number in international format
- When the user initiates the verification process
- Then the system shall generate a cryptographically secure random 6-digit verification code
- And the system shall send the verification code via SMS to the provided phone number
- And the system shall store the verification code hash (not the plain code) with expiration timestamp
- And the system shall enforce rate limiting on SMS code generation (max 3 attempts per 10 minutes per phone number)
- And the system shall record SMS sending attempts for audit and abuse prevention
- And the system shall handle SMS delivery failures gracefully with appropriate user feedback
- And the system shall allow users to request a new verification code after a cool-down period
- And the system shall accept user-entered verification codes for validation
- And the system shall verify that the entered code matches the stored hash and is not expired
- And the system shall provide clear feedback on code validation success or failure
- And the system shall immediately invalidate the verification code after successful validation
- And the system shall log verification code validation attempts for security monitoring

## Explicit Exclusions
- Email-based verification as an alternative to SMS
- Voice call verification as an alternative to SMS
- Verification codes longer than 6 digits
- Alphanumeric verification codes
- Verification code reuse after validation
- International SMS delivery guarantees (reliability varies by carrier and country)

## Constraints
- Must use cryptographically secure random number generation for verification codes
- Must hash verification codes before storage (never store plain codes)
- Must set expiration time for verification codes (10 minutes)
- Must enforce rate limiting to prevent SMS flooding and abuse
- Must use approved SMS gateway providers with proper compliance
- Must include clear sender identification in SMS messages
- Must provide opt-out instructions in SMS messages where required by regulations
- Must handle SMS delivery receipts and failures appropriately
- Must not log or store plain verification codes in any system logs
- Must comply with TCPA and similar regulations for SMS communications
- Must provide accessible error messages for users with disabilities

## Validation Method
- Automated test: Unit tests for verification code generation and hashing
- Automated test: Integration tests for SMS sending and code validation flow
- Manual QA: Testing with actual SMS gateways (in sandbox/test mode)
- Security review: Validation of cryptographic security and code handling
- Architecture review: Confirmation of proper security measures and rate limiting
- Compliance review: Validation of SMS regulatory compliance

## References
Approved artifacts this requirement should be interpreted with.

- Related Requirements, non-blocking:
  - FR-CCEF-018 (Phone Number Input and Validation for Verification)
  - FR-CCEF-020 (SMS Consent Capture and Recording)
  - FR-CCEF-021 (Phone Number Management in Account Settings)
- ADRs:
  - ADR-0001 (Modular Monolith with Clear Boundaries Approach)
- API / Data Contracts:
  - E.164 International Telecommunications Numbering Plan standard
  - Selected SMS gateway provider API specifications (Twilio, AWS SNS, etc.)
- Policies / Regulations:
  - TCPA (Telephone Consumer Protection Act)
  - GDPR Article 32 (Security of processing)
  - NIST SP 800-63B (Digital Identity Guidelines)
- Design Artifacts:
  - ccef-ui-ux/prototype/index.html (SMS verification implementation)
- Other:
  - RFC 4086 (Randomness Requirements for Security)
  - OWASP Authentication Security Guidelines

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