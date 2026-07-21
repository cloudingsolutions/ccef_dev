# Milestone

- Milestone ID: MS-CCEF-001
- Product Slice ID: PS-CCEF-001
- Title: SSO Authentication Foundation
- Lifecycle State: Green-Lit

## Objective

Establish foundational SSO authentication flows for Google and Apple identity providers, including GDPR-compliant consent management, secure session handling, and audit logging. This milestone delivers basic account creation that enables users to access the system without passwords.

## Dependencies

- Predecessor Milestones: None
- Included Requirement IDs: FR-CCEF-001, FR-CCEF-002, FR-CCEF-009, NFR-CCEF-001, NFR-CCEF-009

## Explicit Exclusions

- UC-CCEF-002, UC-CCEF-004, UC-CCEF-005, UC-CCEF-006, UC-CCEF-007, UC-CCEF-008
- FR-CCEF-003 (email one-time code), FR-CCEF-004 (account linking), FR-CCEF-005 (password update), FR-CCEF-006 (basic account settings), FR-CCEF-007 (residency selection)
- FR-CCEF-011 through FR-CCEF-032
- FR-CCEF-010, FR-CCEF-013, FR-CCEF-014, FR-CCEF-016, FR-CCEF-017 (Out of Scope Requirements)
- Phone number collection and verification (covered in Milestone 2)
- Language preference configuration (covered in Milestone 3)
- SMS consent and alert delivery preferences (covered in Milestone 2)
- Deferred/adjacent intent: Organization/team management, advanced authorization, additional languages beyond English/Swedish

## Traceability

- Included Use Case IDs: UC-CCEF-001
- Architectural Assumptions:
  - Module boundaries follow ADR-0001: interface/ is the public contract, impl/ contains private implementation
  - Authentication module will be implemented as a separate module within the modular monolith
  - Token storage will use HSM/KMS integration as specified in NFR-CCEF-001 for cryptographic operations
  - Legal consent records will be signed cryptographically as specified in NFR-CCEF-009
  - Data residency inference will use IP geolocation as minimum European requirement
  - GDPR compliance will be achieved through explicit consent capture and data minimization principles
- Required ADRs: ADR-0001
- Quality Gates:
  - Google SSO flow completes within 2s including redirect back to CCEF (p95 < 800ms token exchange time)
  - Apple SSO flow completes within 2s including redirect back to CCEF (p95 < 800ms token exchange time)
  - All identity tokens validated with < 10ms verification time
  - Session fixation risk eliminated through new session creation after login
  - Audit logs correctly encrypted and include PII hashes for all authentication events
  - User consent explicitly captured and stored with timestamp and version for GDPR compliance
  - 99.9% availability for SSO authentication flows measured over 7-day rolling window
  - No cross-site scripting (XSS) vulnerabilities found in authentication flow UI
  - All OAuth 2.0/OIDC state parameters properly validated to prevent CSRF attacks
- Demo Criteria:
  - User can authenticate with Google SSO and access the post-onboarding flow
  - User can authenticate with Apple SSO and access the post-onboarding flow
  - System correctly creates new accounts linked to SSO identities
  - User receives appropriate error messages for network and user-denial scenarios
  - Audit logs demonstrate proper token validation and consent capture
  - Session management works correctly with secure cookie attributes
  - Directive: Feature flag 'enable_email_password_fallback' is disabled in this milestone
- Acceptance Criteria:
  - User can successfully create an account via Google SSO flow with no password requirement
  - User can successfully create an account via Apple SSO flow with no password requirement
  - System successfully validates Google identity tokens using Google's JWKS and OIDC standards
  - System successfully validates Apple identity tokens using Apple's JWKS with ES256 algorithm
  - Email addresses are normalized to lowercase for account lookup
  - New accounts are created with GDPR-compliant defaults (Europe residency inferred from IP/Phone)
  - User is redirected to post-authentication flow within 2 seconds (±200ms tolerance)
  - Secure session cookies are established with HttpOnly, Secure, and SameSite=Strict attributes
  - GDPR-compliant privacy notice is displayed with explicit opt-in checkbox before data processing
  - Explicit consent is captured, timestamped, and stored for audit purposes
  - Audit logs encrypt PII with AES-256-GCM and include SHA-256 hashes of PII for verification
  - All OAuth 2.0/OIDC state parameters are validated to prevent CSRF and replay attacks
  - User receives appropriate error messages for network failures and user-denied permissions within 500ms
  - System handles both Google SSO JS SDK and REST API/Sign In with Apple REST API flows
  - Users with existing accounts are correctly authenticated without duplicate account creation
  - Session fixation is prevented by creating new session identifiers after login
  - User profile information (email, name) is populated from identity provider and persisted

## Release Branches

1. src: milestone/MS-CCEF-001-sso-authentication-foundation from main

## Artifacts

- Completion Evidence: None.

### Coverage Matrix

| Requirement ID | Covered In This Milestone? | Fully/Partially Covered | Validation Method |
|---|---|---|---|
| FR-CCEF-001 | True | Full | Automated unit/integration tests for token validation; end-to-end testing with Google developer project |
| FR-CCEF-002 | True | Full | Automated unit/integration tests for token validation; end-to-end testing with Apple developer account |
| FR-CCEF-009 | True | Full | Contract tests verifying consent record format and storage; compliance review of consent timestamp and version tracking |
| NFR-CCEF-001 | True | Partial | Review of token storage implementation and KMS/HSM integration plans; security validation of cryptographic operations |
| NFR-CCEF-009 | True | Full | Legal review of consent record cryptographic signing implementation; audit log verification |

### Increment Integrity

- Can this milestone be demoed independently? Yes.
- Can this milestone be deployed safely? Yes.
- What feature flags or disabled paths are required? Email/password fallback authentication is disabled (enabled_email_password_fallback = false); Phone number collection is disabled (enable_phone_collection = false); Language preference configuration is disabled (enable_language_config = false); Password update is disabled (enable_password_update = false)
- What user-visible behavior is intentionally incomplete? GDPR-compliant privacy notice is presented but only specific
