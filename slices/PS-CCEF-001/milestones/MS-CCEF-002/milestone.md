# Milestone

- Milestone ID: MS-CCEF-002
- Product Slice ID: PS-CCEF-001
- Title: Phone Verification and Consent
- Lifecycle State: Approved

## Objective

Enable users to provide and verify their phone number for SMS consent, with explicit opt-in captured for GDPR compliance, while allowing users to skip phone setup during onboarding.

## Dependencies

- Predecessor Milestones: MS-CCEF-001
- Included Requirement IDs: FR-CCEF-018, FR-CCEF-019, FR-CCEF-020, FR-CCEF-021

## Explicit Exclusions

- UC-CCEF-002 (phone number verification for initial account creation - explicitly excluded, but note: this milestone is for optional phone setup after account creation, which is allowed)
- FR-CCEF-008 (password strength requirements - explicitly excluded)
- FR-CCEF-010, FR-CCEF-011, FR-CCEF-012, FR-CCEF-013, FR-CCEF-014, FR-CCEF-016, FR-CCEF-017 (various excluded functional requirements)
- Deferred / adjacent product intent: organization/team management, complex authorization schemes, additional languages, advanced account recovery, social logins beyond Google/Apple, advanced privacy controls, data export, data retention policies, account closure, subscription management, API access, multi-currency, role-based views, audit logging beyond basics, data residency beyond Europe, additional privacy frameworks, onboarding tours, in-app messaging, log aggregation, API rate limiting beyond basics, multi-tenant architecture, data partitioning, accessibility enhancements beyond WCAG 2.2 AA, internationalization frameworks
- SMS alert delivery functionality (covered in other use cases - not in this slice)
- Phone number porting or carrier change handling
- International phone number restrictions based on regulatory requirements
- Voice call verification as alternative to SMS

## Traceability

- Included Use Case IDs: UC-CCEF-004
- Architectural Assumptions:
  - The system follows a modular monolith architecture with clear boundaries (ADR-0001)
  - Phone number verification uses standard SMS gateway APIs
  - Rate limiting is applied per phone number and per IP address to prevent abuse
  - Consent for SMS alerts is stored separately from general data processing consent
  - The system uses AES-256-GCM to encrypt audit log entries containing PII (phone number, consent)
  - HTTP 1.2 or higher is used for all SMS gateway communications
  - The system implements exponential backoff for SMS retries
  - Phone numbers are stored in E.164 format
  - The system implements PKCE for any OAuth flows related to phone verification (if applicable)
  - Secure session cookie attributes are maintained during phone verification step
- Required ADRs: ADR-0001, ADR-0002
- Quality Gates:
  - Phone number validation must comply with E.164 format and prevent duplicates
  - SMS OTP must be time-limited and rate-limited to prevent abuse
  - Explicit consent must be captured before recording SMS opt-in (not pre-checked)
  - Consent must be stored with timestamp and user ID for audit purposes
  - System must allow users to update or remove phone number with appropriate consent handling
  - No phone number may be stored without explicit consent for SMS alerts
  - System must handle SMS delivery failures gracefully with user-friendly error messages
- Demo Criteria:
  - Demonstrate phone number entry and verification flow
  - Show successful SMS code validation
  - Display explicit consent request for SMS alerts and capture opt-in
  - Show confirmation of phone verification and consent completion
  - Demonstrate rate limiting behavior when too many SMS requests are made
  - Show user-friendly error messages for SMS delivery failures
- Acceptance Criteria:
  - User can skip phone setup and continue onboarding without verified phone number or SMS consent
  - If user chooses phone setup, user enters phone number in correct international format
  - System validates phone number format and checks if already associated with another account
  - System sends a one-time verification code via SMS to the provided number
  - User receives the SMS and enters the verification code
  - System validates the code is correct and not expired
  - System marks the phone number as verified for the user's account
  - System presents a clear consent request for SMS alerts
  - User explicitly opts in to receive SMS alerts (not pre-checked)
  - System records the consent with timestamp and user ID for audit purposes
  - User receives confirmation that phone verification and consent are complete
  - System enforces rate limiting on SMS code generation to prevent abuse
  - User can update or remove their phone number in account settings with appropriate consent handling
  - Consent actions are recorded in the audit trail for compliance purposes
  - If SMS delivery, code validation, expiration, or rate limiting prevents completion, the system shows a user-facing error message and recovery action
  - System does not require phone number collection to complete initial account creation

## Release Branches

1. Release branch creation happens only after Human green-light.

## Artifacts

- Completion Evidence: None.

### Coverage Matrix

| Requirement ID | Covered In This Milestone? | Fully/Partially Covered | Validation Method |
|---|---|---|---|
| FR-CCEF-001 | True | Complete | Covered in Milestone 1; verified to still work |
| FR-CCEF-002 | True | Complete | Covered in Milestone 1; verified to still work |
| FR-CCEF-003 | True | Complete | Covered in Milestone 1; verified to still work |
| FR-CCEF-004 | True | Complete | Covered in Milestone 1; verified to still work |
| FR-CCEF-005 | True | Complete | Covered in Milestone 1; verified to still work |
| FR-CCEF-006 | True | Complete | Covered in Milestone 1; verified to still work |
| FR-CCEF-007 | True | Complete | Covered in Milestone 1; verified to still work |
| FR-CCEF-009 | True | Complete | Covered in Milestone 1; verified to still work |
| FR-CCEF-015 | True | Complete | Covered in Milestone 1; verified to still work (phone number format validation) |
| FR-CCEF-018 | True | Complete | Unit tests for phone number format validation; integration tests verifying SMS sending and delivery |
| FR-CCEF-019 | True | Complete | Unit tests for OTP validation logic; integration tests verifying SMS OTP flow |
| FR-CCEF-020 | True | Complete | Unit tests for rate limiting on SMS code generation; integration tests verifying rate-limited behavior |
| FR-CCEF-021 | True | Complete | Unit tests for consent capture logic; integration tests verifying explicit opt-in for SMS alerts |
| FR-CCEF-022 | False | Not Covered | N/A |
| FR-CCEF-023 | False | Not Covered | N/A |
| FR-CCEF-024 | False | Not Covered | N/A |
| FR-CCEF-025 | False | Not Covered | N/A |
| FR-CCEF-026 | False | Not Covered | N/A |
| FR-CCEF-027 | False | Not Covered | N/A |
| FR-CCEF-028 | False | Not Covered | N/A |
| FR-CCEF-029 | False | Not Covered | N/A |
| FR-CCEF-030 | False | Not Covered | N/A |
| FR-CCEF-031 | False | Not Covered | N/A |
| FR-CCEF-032 | False | Not Covered | N/A |
| NFR-CCEF-001 | True | Complete | Covered in Milestone 1; verified to still work |
| NFR-CCEF-002 | True | Complete | Load testing verifying SMS OTP response time < 500ms; overall authentication benchmarks still met |
| NFR-CCEF-003 | True | Complete | Unit tests verifying HTTP 429 with Retry-After header for SMS rate limiting; integration tests simulating rate-limited SMS attempts |
| NFR-CCEF-004 | True | Complete | Covered in Milestone 1; verified to still work |
| NFR-CCEF-005 | True | Complete | Covered in Milestone 1; verified to still work (data residency inference still works) |
| NFR-CCEF-006 | True | Complete | Covered in Milestone 1; verified to still work |
| NFR-CCEF-007 | True | Complete | Covered in Milestone 1; verified to still work |
| NFR-CCEF-008 | False | Not Covered | N/A |
| NFR-CCEF-009 | False | Not Covered | N/A |

### Increment Integrity

- Can this milestone be demoed independently? Yes.
- Can this milestone be deployed safely? Yes.
- What feature flags or disabled paths are required? Language settings beyond English/Swedish are disabled; account settings UI is hidden; legal acceptance and data residency steps are skipped in onboarding if feature flags are off; SMS consent feature can be toggled off
- What user-visible behavior is intentionally incomplete? Language preference is limited to detected browser/OS language (no user selection); legal acceptance and data residency steps are not presented; account settings interface is not accessible; SMS alerts are not sent (only consent is captured)
