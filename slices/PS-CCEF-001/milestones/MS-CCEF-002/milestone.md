# Milestone

- Milestone ID: MS-CCEF-002
- Product Slice ID: PS-CCEF-001
- Title: User Profile & Consent Completion
- Lifecycle State: Approved

## Objective

Enable users to complete their account setup by providing phone number for verification and consent, configuring language preferences, selecting appropriate data residency, and accepting terms and privacy policies. This milestone delivers a fully configured user account ready for system access and basic alerts.

## Dependencies

- Predecessor Milestones: MS-CCEF-001
- Included Requirement IDs: FR-CCEF-003, FR-CCEF-004, FR-CCEF-005, FR-CCEF-006, FR-CCEF-007, FR-CCEF-018, FR-CCEF-019, FR-CCEF-020, FR-CCEF-021, FR-CCEF-011, FR-CCEF-012, FR-CCEF-015, FR-CCEF-018, FR-CCEF-019, FR-CCEF-020, FR-CCEF-021, NFR-CCEF-004, NFR-CCEF-006, NFR-CCEF-007, NFR-CCEF-008

## Explicit Exclusions

- UC-CCEF-004, UC-CCEF-005, UC-CCEF-006, UC-CCEF-007, UC-CCEF-008
- FR-CCEF-018 through FR-CCEF-032
- Advanced account recovery and password management (covered in future milestones)
- Organization/team management and multi-user roles (covered in future milestones)

## Traceability

- Included Use Case IDs: UC-CCEF-003, UC-CCEF-004
- Architectural Assumptions:
  - Phone verification service will integrate with SMS gateway provider
  - Language detection logic will be implemented in the frontend layer
  - Residency inference will use IP geolocation with fallback to phone number country codes
  - Account settings module will reuse authentication session established in MS-CCEF-001
  - Legal consent module will build upon NFR-CCEF-009 implementation from MS-CCEF-001
- Required ADRs: ADR-0001, ADR-0002
- Quality Gates:
  - Phone number OTP verification response time < 200ms p95
  - Language preference configuration completes without errors
  - Residency inference correctly identifies minimum European region as default
  - Terms and privacy policy acceptance captured with explicit user action
  - Legal consent records cryptographically signed and verifiable
  - 99.9% availability for account configuration flows measured over 7-day rolling window
  - No accessibility violations found in account configuration UI (WCAG 2.2 AA baseline)
  - SMS consent only captured after successful phone verification
  - Device language detection works for major browsers (Chrome, Safari, Firefox, Edge)
- Demo Criteria:
  - User can complete phone number verification flow with OTP
  - User can configure language preferences (English/Swedish)
  - User can configure residency requirements
  - Terms and conditions are explicitly accepted
  - Basic account settings can be updated
  - User successfully reaches 'ready to use' state after this milestone
  - Directive: Password update enabled only for existing users in this milestone
  - Directive: Email/password fallback authentication available but not required for completion
- Acceptance Criteria:
  - User can provide and verify a phone number via OTP during onboarding
  - System captures explicit consent for SMS alerts based on verified phone number
  - Consent for SMS alerts is cryptographically signed and stored with audit trail
  - User can configure language preferences (English/Swedish) during account setup
  - Device/OS language is detected and pre-selected during onboarding
  - User can override detected device language during onboarding flow
  - Language preference is changeable post-onboarding in account settings
  - System correctly infers data residency from IP address and phone number
  - Users can select region where permitted (Europe minimum, additional regions per legal requirements)
  - Terms & conditions and privacy policy are displayed with required explicit acceptance
  - GDPR-compliant privacy notice is presented for data processing consent
  - Legal consent records are cryptographically verifiable through digital signatures
  - Basic account settings can be updated (name, contact preferences)
  - User receives success message upon account completion
  - Phone number OTP verification completes within 200ms response time
  - Language configuration completes without user-visible errors
  - Residency selection prevents silent assignment to unsupported regions
  - Clear error messages presented for failed OTP verification

## Release Branches

1. Release branch creation happens only after Human green-light.

## Artifacts

- Completion Evidence: None.

### Coverage Matrix

| Requirement ID | Covered In This Milestone? | Fully/Partially Covered | Validation Method |
|---|---|---|---|
| FR-CCEF-003 | True | Full | Automated tests for email OTP generation, delivery, and verification; integration tests with email provider |
| FR-CCEF-004 | True | Full | Contract tests verifying consent record storage and retrieval; legal review of consent evidence |
| FR-CCEF-005 | True | Full | Tests for device language detection, user override, and persistent storage; acceptance tests for language preference changes |
| FR-CCEF-006 | True | Full | Tests for residency inference from IP and phone number; validation of user selection where permitted; tests preventing unsupported region assignment |
| FR-CCEF-007 | True | Full | Tests for clear terms/conditions and privacy policy presentation; acceptance tests for explicit acceptance requirement |
| FR-CCEF-011 | True | Full | Tests for basic account settings updates (name, contact preferences); integration tests with user profile module |
| FR-CCEF-012 | True | Full | Tests for name/password update flows; acceptance tests for validation and error handling |
| FR-CCEF-015 | True | Full | Tests verifying that phone number must be verified before SMS alerts can be sent; acceptance tests for consent requirement |
| NFR-CCEF-004 | True | Full | Performance tests measuring OTP verification response times; compliance review of timing requirements |
| NFR-CCEF-006 | True | Full | Reviews of accessibility requirements compliance; manual QA testing |
| NFR-CCEF-007 | True | Full | Tests verifying responsive design across mobile, tablet, small desktop, and desktop layouts |
| NFR-CCEF-008 | True | Full | Tests for fallback English presentation when device language detection fails; manual QA for localization coverage |

### Increment Integrity

- Can this milestone be demoed independently? Yes.
- Can this milestone be deployed safely? Yes.
- What feature flags or disabled paths are required? SMS alert delivery channels beyond onboarding consent capture are disabled (enable_sms_delivery = false); Advanced account settings (password update) are enabled only for existing users, not new signups; Email/password fallback flow may be enabled for testing but disabled by default
- What user-visible behavior is intentionally incomplete? Language selection includes only English and Swedish (additional languages reserved for future milestone); Residency selection includes Europe as minimum with specific legal region restrictions to be defined per jurisdiction
