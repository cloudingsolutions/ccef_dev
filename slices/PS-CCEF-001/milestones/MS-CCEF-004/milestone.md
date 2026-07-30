# Milestone

- Milestone ID: MS-CCEF-004
- Product Slice ID: PS-CCEF-001
- Title: Account Settings Management
- Lifecycle State: Ready for Approval

## Objective

Enable authenticated users to view and update their basic account information including name, language preference, and contact preferences through a secure account settings interface with validation, persistence, and audit trails.

## Dependencies

- Predecessor Milestones: MS-CCEF-003
- Included Requirement IDs: FR-CCEF-024, FR-CCEF-025, FR-CCEF-026, FR-CCEF-027, FR-CCEF-028, FR-CCEF-029, FR-CCEF-030

## Explicit Exclusions

- UC-CCEF-002 (Out of Scope - covered in UC-CCEF-001 for both Google and Apple SSO)
- FR-CCEF-008, FR-CCEF-010, FR-CCEF-011, FR-CCEF-012, FR-CCEF-013, FR-CCEF-014, FR-CCEF-016, FR-CCEF-017 (Out of Scope functional requirements)
- UC-CCEF-009 and beyond (if any exist)
- Deferred / adjacent product intent: organization/team management, complex authorization schemes, additional languages beyond English/Swedish, advanced account recovery, social login beyond Google/Apple, advanced privacy controls, data export, data retention policies, account closure, subscription management, API access, multi-currency, role-based views, audit logging for compliance, data residency beyond Europe, additional privacy frameworks, onboarding flows beyond account creation, product tours, in-app messaging, log aggregation, API rate limiting, multi-tenant architecture, data partitioning, accessibility enhancements beyond WCAG 2.2 AA, internationalization frameworks.
- Advanced profile information (profile picture, bio, etc.)
- Social media account linking/unlinking
- Two-factor authentication setup or management
- Data export or deletion requests (covered in privacy use cases)
- Payment method or billing information management
- Provider connection management (covered in other slices)
- Account closure or deletion (deferred to later slice)
- Language preferences beyond English and Swedish
- Phone number verification and SMS consent setup (covered in Milestone 2 - note: contact preferences in this milestone are for email notifications, not SMS)
- Data residency confirmation (covered in Milestone 3)
- Language selection and legal acceptance (covered in Milestone 1)

## Traceability

- Included Use Case IDs: UC-CCEF-006
- Architectural Assumptions:
  - The system follows a modular monolith approach with clear boundaries as defined in ADR-0001.
  - GDPR-compliant data handling practices are implemented as specified in ADR-0002, including consent management and data residency controls.
  - The system uses a user management module for storing and retrieving user profile information (name, email, language preference, etc.).
  - Contact preferences are stored as part of the user profile or in a dedicated preferences module.
  - The system uses a separate privacy module for managing consent records as outlined in ADR-0002.
  - All user profile updates go through validation and authorization checks before being persisted.
  - Audit logging captures all account modification attempts for compliance and security monitoring.
  - Language preference is stored as part of the user profile and used for UI localization throughout the system.
  - Residency region is stored as part of the user profile but is display-only in account settings after onboarding.
  - The system maintains separation between editable profile information (name, language, contact preferences) and immutable onboarding data (auto-inferred residency, legal acceptance timestamps).
  - The system implements immediate UI updates for language preference changes without requiring full page reload.
  - Input validation is performed both client-side (for immediate feedback) and server-side (for security).
- Required ADRs: ADR-0001, ADR-0002
- Quality Gates:
  - Code review by system architect and security specialist
  - Unit test coverage ≥ 90% for new functionality
  - Integration tests covering name update, language preference change, contact preferences modification, and validation flows
  - End-to-end test scenarios for account settings usage
  - Security review focusing on input validation, authorization checks, and data protection for profile updates
  - Compliance review verifying GDPR adherence for handling of personal data in account settings
  - Performance testing for account settings load and save operations under expected user load
  - Accessibility testing (WCAG 2.2 AA) for form inputs, validation feedback, and language change announcements
  - User acceptance testing with representative users for account settings usage and preference updates
- Demo Criteria:
  - Demonstrate viewing account information: navigate to account settings after login and see current name, email, and language preference displayed.
  - Demonstrate name update: enter new valid display name, save changes, and see confirmation with updated name displayed throughout interface.
  - Demonstrate language preference change: select alternative language (English/Swedish), save changes, and see immediate interface translation.
  - Demonstrate contact preferences update: toggle email notification switches, save changes, and see confirmation.
  - Demonstrate validation error handling: enter invalid name (too short, special characters), see clear error messages and field highlighting.
  - Demonstrate audit trail recording: verify that account modification attempts (successful and failed) are recorded in audit trail (via admin interface or logs).
  - Demonstrate persistence across sessions: log out and log back in, verify that updated name and language preference are retained.
  - Demonstrate accessibility announcements: use screen reader to verify language change is announced when preference is updated.
  - Demonstrate residency display-only: navigate to account settings and see residency region displayed but not editable.
  - Demonstrate immediate UI update: change language preference and observe instant translation without page reload flicker.
- Acceptance Criteria:
  - Authenticated user can view their current account information (name, email, language preference) in account settings.
  - User can update their display name with validation (reasonable length, no prohibited characters).
  - User can update their default language preference (English/Swedish) and see immediate interface update.
  - User can manage basic contact preferences (email notifications, etc.) through toggle switches or similar controls.
  - System validates all inputs before saving changes (name format, language selection, etc.).
  - System provides immediate feedback on success or validation errors (inline messages, field highlighting).
  - Changed information persists across sessions and is reflected throughout the interface after reload.
  - System maintains audit trail of account modification attempts (both successful and failed).
  - User receives confirmation when changes are successfully saved (toast/banner notification).
  - Invalid inputs are rejected with clear, specific error messages (e.g., 'Name must be between 2 and 50 characters').
  - Account modification attempts are recorded in the audit trail with timestamp, user ID, and changed fields.
  - Language preference change triggers appropriate accessibility announcements for screen reader users.
  - Contact preference changes are recorded and affect future notification delivery (where applicable).
  - System does not allow modification of residency region after onboarding (display-only in account settings).
  - System does not allow modification of consent settings for SMS in account settings (handled via separate flow if needed).
  - Advanced profile information (profile picture, bio, etc.) is not available in this slice.
  - Social media account linking/unlinking is not available in this slice.
  - Two-factor authentication setup or management is not available in this slice.
  - Data export or deletion requests are not available in this slice (covered in privacy use cases).
  - Payment method or billing information management is not available in this slice.
  - Provider connection management is not available in this slice (covered in other slices).
  - Account closure or deletion is not available in this slice (deferred to later slice).
  - Language preferences beyond English and Swedish are not available in this slice.

## Release Branches

1. Release branch creation happens only after Human green-light.

## Artifacts

- Completion Evidence: None.

### Coverage Matrix

| Requirement ID | Covered In This Milestone? | Fully/Partially Covered | Validation Method |
|---|---|---|---|
| FR-CCEF-024 | True | Full | Unit tests for display name validation, integration tests with user repository, end-to-end test scenarios for name update. |
| FR-CCEF-025 | True | Full | Unit tests for language preference validation, integration tests with user repository, end-to-end test scenarios for language preference update. |
| FR-CCEF-026 | True | Full | Unit tests for contact preferences validation, integration tests with preferences repository, end-to-end test scenarios for email notification toggle. |
| FR-CCEF-027 | True | Full | Unit tests for input validation service, integration tests with validation rules, end-to-end test scenarios for combined field validation. |
| FR-CCEF-028 | True | Full | Unit tests for real-time validation feedback, integration tests with UI components, end-to-end test scenarios for inline error display. |
| FR-CCEF-029 | True | Full | Unit tests for persistence layer, integration tests with user/preferences repositories, end-to-end test scenarios for data persistence across sessions. |
| FR-CCEF-030 | True | Full | Unit tests for success confirmation service, integration tests with notification system, end-to-end test scenarios for toast/banner display after save. |

### Increment Integrity

- Can this milestone be demoed independently? Yes.
- Can this milestone be deployed safely? Yes.
- What feature flags or disabled paths are required? Advanced profile features (picture, bio, etc.) are disabled/not available; social media linking is disabled/not available; 2FA setup is disabled/not available; data export/deletion is disabled/not available; payment/billing management is disabled/not available; provider connection management is disabled/not available; account closure/deletion is disabled/not available; language preferences beyond English/Swedish are disabled/not available.
- What user-visible behavior is intentionally incomplete? Users cannot add profile pictures or bios; users cannot link/unlink social media accounts; users cannot set up or manage two-factor authentication; users cannot export or delete their data; users cannot manage payment methods or billing information; users cannot manage provider connections; users cannot close or delete their accounts; users cannot select language preferences beyond English or Swedish.
