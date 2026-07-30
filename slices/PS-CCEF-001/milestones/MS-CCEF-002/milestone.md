# Milestone

- Milestone ID: MS-CCEF-002
- Product Slice ID: PS-CCEF-001
- Title: Phone Verification and SMS Consent with Enhanced Security
- Lifecycle State: Ready for Approval

## Objective

Enable users to provide and verify their phone number for SMS consent after account creation, with explicit opt-in consent capture and audit trails for GDPR compliance, including cryptographic signing and append-only storage for consent record integrity.

## Dependencies

- Predecessor Milestones: MS-CCEF-001
- Included Requirement IDs: FR-CCEF-018, FR-CCEF-019, FR-CCEF-020, FR-CCEF-021

## Explicit Exclusions

- UC-CCEF-002 (Out of Scope - covered in UC-CCEF-001 for both Google and Apple SSO)
- FR-CCEF-008, FR-CCEF-010, FR-CCEF-011, FR-CCEF-012, FR-CCEF-013, FR-CCEF-014, FR-CCEF-016, FR-CCEF-017 (Out of Scope functional requirements)
- UC-CCEF-009 and beyond (if any exist)
- Deferred / adjacent product intent: organization/team management, complex authorization schemes, additional languages beyond English/Swedish, advanced account recovery, social login beyond Google/Apple, advanced privacy controls, data export, data retention policies, account closure, subscription management, API access, multi-currency, role-based views, audit logging for compliance, data residency beyond Europe, additional privacy frameworks, onboarding flows beyond account creation, product tours, in-app messaging, log aggregation, API rate limiting, multi-tenant architecture, data partitioning, accessibility enhancements beyond WCAG 2.2 AA, internationalization frameworks.
- SMS alert delivery functionality (the actual sending of SMS alerts to users) is disabled/not available; data residency confirmation is disabled/not available; account settings for updating name, language, and contact preferences are disabled/not available.
- Phone number porting or carrier change handling
- International phone number restrictions based on regulatory requirements
- Voice call verification as alternative to SMS
- Requiring phone number collection to complete initial account creation (explicitly excluded per UC-CCEF-004)
- Account settings for updating name, language, and contact preferences (covered in Milestone 4)
- Data residency confirmation (covered in Milestone 3)
- Language selection and legal acceptance (covered in Milestone 1)

## Traceability

- Included Use Case IDs: UC-CCEF-004
- Architectural Assumptions:
  - The system follows a modular monolith approach with clear boundaries as defined in ADR-0001.
  - GDPR-compliant data handling practices are implemented as specified in ADR-0002, including consent management for communications.
  - Phone number verification uses a trusted SMS provider API with secure credential storage.
  - The system uses a separate module for privacy and consent management as outlined in ADR-0002.
  - Phone numbers are stored in encrypted format in the user profile or a dedicated privacy module.
  - SMS sending infrastructure is isolated and configured with approved providers only.
  - Rate limiting is implemented at the API gateway or service level to prevent abuse.
  - All consent actions are auditable and linked to specific user IDs and timestamps with cryptographic signing.
  - Consent records are stored with append-only storage to ensure immutability and prevent unauthorized modification.
  - Phone number verification does not affect core authentication or account access.
  - The system maintains separation between phone number for SMS consent and other potential future uses (e.g., 2FA).
- Required ADRs: ADR-0001, ADR-0002
- Quality Gates:
  - Code review by system architect and security specialist
  - Unit test coverage ≥ 90% for new functionality
  - Integration tests covering phone number validation, SMS sending, OTP validation, and consent capture flows
  - End-to-end test scenarios for phone verification and consent process
  - Security review focusing on phone number data protection, consent management, cryptographic signing, append-only storage, and SMS provider integration security
  - Compliance review verifying GDPR adherence for consent collection and audit trail requirements, including consent record integrity verification
  - Performance testing for SMS code generation rate limiting under load
  - Accessibility testing (WCAG 2.2 AA) for phone number input and verification flow
  - User acceptance testing with representative users for phone verification and consent opt-in/out
- Demo Criteria:
  - Demonstrate phone number entry: navigate to phone setup after account creation, enter valid international phone number, and proceed to verification.
  - Demonstrate SMS OTP receipt: simulate receiving SMS with verification code, enter code, and see success message.
  - Demonstrate consent opt-in: after successful verification, explicitly opt in to SMS alerts and see confirmation.
  - Demonstrate consent audit trail: verify that consent grant is recorded with timestamp, user ID, and cryptographic signature (via admin interface or logs).
  - Demonstrate skip option: choose to skip phone setup and continue to core functionality without verification.
  - Demonstrate error handling: test invalid phone number format, failed SMS delivery, expired OTP, and rate limiting scenarios to see appropriate user-facing error messages.
  - Demonstrate phone number update: navigate to account settings, update phone number, go through verification flow again, and confirm change.
  - Demonstrate consent integrity: verify that SMS consent records cannot be tampered with due to cryptographic signing and append-only storage.
- Acceptance Criteria:
  - User is offered phone setup after account creation without blocking account creation completion.
  - User can skip phone setup and continue onboarding without verified phone number or SMS consent.
  - If the user chooses phone setup, user enters their phone number in the correct international format (E.164).
  - System validates phone number format and checks if already associated with another account.
  - System sends a one-time verification code via SMS to the provided number using an approved SMS provider.
  - User receives the SMS and enters the verification code.
  - System validates the code is correct and not expired.
  - System marks the phone number as verified for the user's account.
  - System presents a clear consent request for SMS alerts (not pre-checked).
  - User explicitly opts in to receive SMS alerts.
  - System records the consent with timestamp, user ID, phone number, and consent version for audit purposes.
  - System stores SMS consent records in an immutable audit trail with cryptographic signing and append-only storage to prevent tampering.
  - User receives confirmation that phone verification and consent are complete.
  - System enforces rate limiting on SMS code generation to prevent abuse.
  - User can update or remove their phone number in account settings with appropriate consent handling (if consent changed).
  - Consent actions (grant, withdrawal) are recorded in the audit trail for compliance purposes with cryptographic signing.
  - If SMS delivery fails, code validation fails, code expires, or rate limiting triggers, the system shows a user-facing error message and recovery action.
  - System does not silently assign users to arbitrary regions when residency cannot be determined (handled in Milestone 3).

## Release Branches

1. Release branch creation happens only after Human green-light.

## Artifacts

- Completion Evidence: None.

### Coverage Matrix

| Requirement ID | Covered In This Milestone? | Fully/Partially Covered | Validation Method |
|---|---|---|---|
| FR-CCEF-018 | True | Full | Unit tests for phone number format validation (E.164), integration tests with mock SMS provider, end-to-end test scenarios for phone number submission. |
| FR-CCEF-019 | True | Full | Unit tests for SMS code generation and sending, integration tests with mock SMS provider, end-to-end test scenarios for OTP delivery and timing. |
| FR-CCEF-020 | True | Full | Unit tests for OTP validation (correctness, expiration, reuse prevention), integration tests with mock SMS provider, end-to-end test scenarios for code validation. |
| FR-CCEF-021 | True | Full | Unit tests for consent recording service, integration tests with consent repository, end-to-end test scenarios for SMS consent capture and withdrawal with cryptographic signing and append-only storage. |

### Increment Integrity

- Can this milestone be demoed independently? Yes.
- Can this milestone be deployed safely? Yes.
- What feature flags or disabled paths are required? SMS alert delivery (sending actual SMS alerts to users) is disabled/not available; data residency confirmation is disabled/not available; account settings for updating name, language, and contact preferences are disabled/not available.
- What user-visible behavior is intentionally incomplete? Users cannot receive actual SMS alerts (the SMS sending functionality for alerts is not implemented); users cannot confirm or select data residency region; users cannot update account settings after creation (name, language, contact preferences); language selection beyond English/Swedish is not available.
