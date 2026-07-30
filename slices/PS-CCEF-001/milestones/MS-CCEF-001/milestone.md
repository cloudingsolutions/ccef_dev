# Milestone

- Milestone ID: MS-CCEF-001
- Product Slice ID: PS-CCEF-001
- Title: Foundation Account Creation with Language and Accessible Legal Acceptance
- Lifecycle State: Ready for Approval

## Objective

Enable users to create accounts via Google/Apple SSO or email+OTP, select language preference (English/Swedish), and accept required legal terms (terms & conditions and privacy policy) before account completion using accessible mechanisms that comply with WCAG 2.2 AA and GDPR.

## Dependencies

- Predecessor Milestones: None
- Included Requirement IDs: FR-CCEF-001, FR-CCEF-002, FR-CCEF-003, FR-CCEF-004, FR-CCEF-005, FR-CCEF-006, FR-CCEF-007, FR-CCEF-009, FR-CCEF-015, FR-CCEF-022, FR-CCEF-023, FR-CCEF-031, NFR-CCEF-001, NFR-CCEF-002, NFR-CCEF-003, NFR-CCEF-004, NFR-CCEF-005, NFR-CCEF-006, NFR-CCEF-007, NFR-CCEF-008, NFR-CCEF-009

## Explicit Exclusions

- UC-CCEF-002 (Apple SSO use case is actually included; correction: UC-CCEF-002 is Out of Scope but not referenced - UC-CCEF-001 covers both Google and Apple SSO)
- FR-CCEF-008 (Enforce Password Strength Requirements - Out of Scope)
- FR-CCEF-010, FR-CCEF-011, FR-CCEF-012, FR-CCEF-013, FR-CCEF-014, FR-CCEF-016, FR-CCEF-017 (various Out of Scope functional requirements)
- UC-CCEF-009 and beyond (if any exist, but only UC-CCEF-001 through UC-CCEF-008 are defined)
- Deferred / adjacent product intent: organization/team management, complex authorization schemes, additional languages beyond English/Swedish, advanced account recovery, social login beyond Google/Apple, advanced privacy controls, data export, data retention policies, account closure, subscription management, API access, multi-currency, role-based views, audit logging for compliance, data residency beyond Europe, additional privacy frameworks, onboarding flows beyond account creation, product tours, in-app messaging, log aggregation, API rate limiting, multi-tenant architecture, data partitioning, accessibility enhancements beyond WCAG 2.2 AA, internationalization frameworks.
- Phone number verification and SMS consent setup (covered in Milestone 2)
- Data residency confirmation (covered in Milestone 3)
- Account settings for updating name, language, and contact preferences (covered in Milestone 4)

## Traceability

- Included Use Case IDs: UC-CCEF-001, UC-CCEF-003, UC-CCEF-005, UC-CCEF-007
- Architectural Assumptions:
  - The system follows a modular monolith approach with clear boundaries as defined in ADR-0001.
  - GDPR-compliant data handling practices are implemented as specified in ADR-0002, including consent management and data residency controls.
  - SSO tokens are securely stored using encryption/KMS design as specified in ADR-0003.
  - The system uses a distributed architecture with separate modules for authentication, user management, privacy, and audit logging.
  - All personal data processing requires explicit user consent as captured during onboarding.
  - The system maintains audit trails for all significant user actions and system events for compliance and security monitoring.
  - Language preference is stored as part of the user profile and used for UI localization.
  - Legal document versions are tracked and associated with user acceptance records.
  - Legal consent records are stored with cryptographic signing and append-only storage to ensure integrity and prevent tampering.
  - The system implements accessible legal acceptance mechanisms that comply with WCAG 2.2 AA standards.
- Required ADRs: ADR-0001, ADR-0002, ADR-0003
- Quality Gates:
  - Code review by system architect and security specialist
  - Unit test coverage ≥ 90% for new functionality
  - Integration tests covering all SSO, email+OTP, language, and legal acceptance flows
  - End-to-end test scenarios for account creation via all supported methods
  - Security review focusing on consent handling, data protection, secure token storage, and cryptographic signing of consent records
  - Compliance review verifying GDPR adherence for consent collection and legal document handling, including WCAG 2.2 AA accessibility
  - Performance testing for account creation flow under expected load
  - Accessibility testing (WCAG 2.2 AA) for language selection and legal document interaction
  - User acceptance testing with representative users for account creation and language selection
- Demo Criteria:
  - Demonstrate account creation via Google SSO: click 'Continue with Google', authenticate with Google account, be redirected back to CCEF, and see success message.
  - Demonstrate account creation via Apple SSO: click 'Continue with Apple', authenticate with Apple account, be redirected back to CCEF, and see success message.
  - Demonstrate account creation via email+OTP: enter email, receive OTP code, enter code, and see success message.
  - Demonstrate language selection: toggle between English and Swedish during account creation flow and observe UI text translation.
  - Demonstrate legal acceptance: view terms & conditions and privacy policy, check the acceptance checkboxes (which become enabled after viewing), and proceed with account creation.
  - Demonstrate language persistence: log out and log back in, verify interface remains in selected language.
  - Demonstrate audit log verification: check that account creation and consent actions are recorded in audit trail with cryptographic signatures (via admin interface or logs).
  - Demonstrate accessible legal acceptance: verify that legal acceptance checkboxes are accessible via keyboard and screen readers.
- Acceptance Criteria:
  - User can create an account using Google SSO with successful redirect, authentication token validation, account creation, and audit logging.
  - User can create an account using Apple SSO with successful redirect, authentication token validation, account creation, and audit logging.
  - User can create an account using email+OTP with email validation, OTP generation and validation, account creation, and audit logging.
  - User can select language preference (English or Swedish) during account creation flow, with browser/OS language detection and pre-selection.
  - User's selected language preference is persisted and used to display the account creation interface and legal documents.
  - User is presented with clear, readable versions of terms & conditions and privacy policy in their selected language.
  - User can accept terms & conditions and privacy policy via an always-enabled checkbox (not pre-checked) that becomes checkable after viewing the documents.
  - User cannot proceed with account creation without accepting both terms & conditions and privacy policy.
  - System records acceptance of both documents with timestamp, user ID, and document version for audit purposes.
  - User receives confirmation that legal agreements have been accepted.
  - Links to view full documents are accessible from account settings for future reference.
  - Acceptance actions are recorded in the audit trail for compliance purposes with cryptographic signing and append-only storage.
  - All user-facing text in the account creation flow translates to the selected language (English/Swedish).
  - System provides appropriate accessibility announcements for language changes for screen reader users.

## Release Branches

1. Release branch creation happens only after Human green-light.

## Artifacts

- Completion Evidence: None.

### Coverage Matrix

| Requirement ID | Covered In This Milestone? | Fully/Partially Covered | Validation Method |
|---|---|---|---|
| FR-CCEF-001 | True | Full | Unit tests for OAuth2/OIDC flows, integration tests with mock SSO providers, end-to-end test scenarios for account creation via SSO. |
| FR-CCEF-002 | True | Full | Unit tests for OAuth2/OIDC flows, integration tests with mock Apple SSO provider, end-to-end test scenarios for account creation via Apple SSO. |
| FR-CCEF-003 | True | Full | Unit tests for email validation, OTP generation and validation, integration tests with mock email service, end-to-end test scenarios for email+OTP account creation. |
| FR-CCEF-004 | True | Full | Unit tests for account creation service, integration tests with user repository, end-to-end test scenarios for account creation. |
| FR-CCEF-005 | True | Full | Unit tests for consent recording service, integration tests with consent repository, end-to-end test scenarios for consent capture during onboarding. |
| FR-CCEF-006 | True | Full | Unit tests for basic account settings retrieval, integration tests with user repository, end-to-end test scenarios for viewing account information. |
| FR-CCEF-007 | True | Full | Unit tests for audit logging service, integration tests with audit repository, end-to-end test scenarios for audit log creation during account creation and consent capture. |
| FR-CCEF-009 | True | Full | Unit tests for rate limiting on OTP generation, integration tests with mock email service, end-to-end test scenarios for OTP resend limits. |
| FR-CCEF-015 | True | Full | Unit tests for audit trail persistence, integration tests with audit repository, end-to-end test scenarios for audit log verification. |
| FR-CCEF-022 | True | Full | Unit tests for language detection service, integration tests with user repository, end-to-end test scenarios for language preference selection and persistence. |
| FR-CCEF-023 | True | Full | Unit tests for language preference validation, integration tests with user repository, end-to-end test scenarios for language selection (English/Swedish only). |
| FR-CCEF-031 | True | Full | Unit tests for legal document presentation service, integration tests with document repository, end-to-end test scenarios for terms & conditions and privacy policy acceptance with accessible checkbox interaction. |
| NFR-CCEF-001 | True | Full | Security tests for SSO token encryption, key management validation, constant-time operations verification. |
| NFR-CCEF-002 | True | Full | Security tests for SSO token storage implementation, access control verification, token expiration handling. |
| NFR-CCEF-003 | True | Full | Security tests for rate limiting implementation, OTP resend limits, login attempt thresholds, abuse prevention verification. |
| NFR-CCEF-004 | True | Full | Performance tests for account creation flow under load, response time validation, scalability verification. |
| NFR-CCEF-005 | True | Full | Security tests for input validation and sanitization, injection attack prevention, XSS/CSRF protection verification. |
| NFR-CCEF-006 | True | Full | Security tests for secure headers implementation, HTTPS enforcement, secure cookie settings verification. |
| NFR-CCEF-007 | True | Full | Compliance tests for GDPR adherence, consent management verification, data subject rights facilitation. |
| NFR-CCEF-008 | True | Full | Performance tests for language switching functionality, UI update latency verification, accessibility compliance testing. |
| NFR-CCEF-009 | True | Full | Compliance tests for legal acceptance audit trail, document version tracking, cryptographic signing verification, append-only storage verification, retention policy verification. |

### Increment Integrity

- Can this milestone be demoed independently? Yes.
- Can this milestone be deployed safely? Yes.
- What feature flags or disabled paths are required? Phone verification and SMS consent features are disabled/not available; data residency confirmation is disabled/not available; account settings for updating name, language, and contact preferences are disabled/not available.
- What user-visible behavior is intentionally incomplete? Users cannot verify phone number for SMS consent; users cannot confirm or select data residency region; users cannot update account settings after creation (name, language, contact preferences); SMS alert delivery preferences cannot be configured.
