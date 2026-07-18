# Requirement

- Requirement ID: FR-CCEF-002
- Title: Support Apple SSO Account Creation
- Requirement Type: functional
- Product Slice IDs: PS-CCEF-001
- Lifecycle State: Approved

## Requirement Statement
The system shall support account creation via Apple Single Sign-On (SSO) provider.

## Rationale
Users should be able to create accounts using their existing Apple identity for convenience and security, particularly important for users in the Apple ecosystem. This provides choice in authentication methods and aligns with platform expectations for Apple device users.

## Acceptance Criteria
- Given a user on the account creation or sign-in page
- When the user clicks the "Continue with Apple" button
- Then the system shall initiate the Apple Sign In flow using either Apple's JavaScript SDK or REST API
- And after successful Apple authentication, the system shall receive an identity token and authorization code from Apple
- And the system shall validate the identity token signature, expiration, audience, and issuer claims using Apple's public keys
- And the system shall extract the user's email (if shared) and full name from the validated identity token
- And the system shall handle the case where the user chooses to hide their email (receiving a proxy@icloud.com address)
- And the system shall normalize any shared email address to lowercase for account lookup
- And the system shall check if a user account already exists for the Apple account (by email or sub claim)
- And if no account exists, the system shall create a new user account linked to the Apple identity
- And if an account exists, the system shall authenticate the existing user (if not already authenticated)
- And the system shall establish an authenticated session for the user with appropriate session identifier
- And the system shall create a new session identifier after login to prevent session fixation
- And the system shall set secure session cookie attributes (HttpOnly, Secure, SameSite=Strict)
- And the system shall redirect the user to the post-authentication flow (onboarding or main app) within 2 seconds (±200ms tolerance)
- And the system shall clear any transient authentication state after successful completion
- And the system shall handle the case where the user cancels the Apple Sign In sheet or dialog by displaying the exact message "Apple sign-in was cancelled – please try again" within 500ms and logging event code AUTH_DENIED
- And the system shall handle network failures or timeouts during the Apple authentication flow by displaying the exact message "Network error – please try again later" within 500ms and logging the event with timeout duration and event code AUTH_NETWORK_ERROR
- And the system shall properly initialize and validate the nonce parameter to prevent replay attacks
- And the system shall generate and validate the client secret for REST API flows using ES256 algorithm
- And the system shall present a GDPR-compliant privacy notice in a modal dialog requiring an explicit "I agree" checkbox action before proceeding, and shall record the checkbox state, timestamp, and notice version
- And the system shall obtain and record explicit user consent for processing personal data (email, name) through an explicit opt-in action (checkbox selection) and shall store the consent timestamp, version, and user's consent decision
- And the system shall store consent timestamp and version for audit purposes
- And the system shall encrypt audit log entries containing PII with AES-256-GCM
- And the system shall include a SHA-256 hash of PII fields in audit logs for verification

## Explicit Exclusions
- Password creation or management for Apple SSO accounts (handled by Apple)
- Manual email verification for Apple SSO accounts (email verification is handled by Apple)
- Collection of additional profile information beyond email and basic name during SSO flow
- Support for advanced Apple Sign In features like real-time user notification or state updates
- Handling of authorization revocation requests (covered by separate requirements)
- Support for Sign In with Apple on native mobile applications (web-only in this slice)

## Constraints
- Must implement Sign In with Apple according to Apple's official documentation
- Must validate identity tokens using Apple's published JSON Web Key Set (JWKS)
- Must support both the JS SDK and REST API variants of Sign In with Apple
- Must generate and validate the client secret for REST API flows using ES256 algorithm
- Must use HTTPS for all communications with Apple's authentication endpoints
- Must implement proper nonce handling to prevent replay attacks
- Must respect the user's email privacy choice (hide or share real email)
- Must handle the case where user chooses not to share email with the developer
- Must use Apple's registered redirect URIs for the authentication flow
- Must comply with Apple's Developer Program License Agreement and App Store Review Guidelines
- Must not store Apple identity tokens longer than necessary for the authentication flow
- Must enforce Content Security Policy headers
- Must enforce X-Frame-Options to prevent clickjacking
- Must enforce TLS version 1.2 or higher for all provider communications
- Must store user profile data (email, name) in compliance with GDPR data minimization principles
- Must retain user profile data only as long as necessary for account functionality
- Must implement pseudonymization of audit logs containing PII
- Must maintain records of processing activities for personal data (GDPR Art. 30)
- Must conduct Data Protection Impact Assessment for SSO authentication flows
- Must implement breach detection and notification procedures (GDPR Art. 33-34)
- Must ensure cross-border data transfers comply with GDPR Chapter V (SCCs/DPAs)
- Must apply privacy-by-design and privacy-by-default principles

## Validation Method
- Automated test: Unit tests for token validation and signature verification logic
- Automated test: Integration tests simulating the complete Apple SSO flow (both JS SDK and REST API)
- Manual QA: End-to-end testing with actual Apple Developer account
- Security review: Validation of cryptographic validation and secret handling
- Architecture review: Confirmation of proper separation of concerns in auth implementation
- Compliance review: Verification of adherence to Apple's Sign In with Apple requirements

## References
Approved artifacts this requirement should be interpreted with.

- Related Requirements, non-blocking:
  - FR-CCEF-001 (Google SSO support)
  - FR-CCEF-003 (Email one-time code fallback)
  - FR-CCEF-004 (Account linking/unlinking)
- ADRs:
  - ADR-0001 (Modular Monolith with Clear Boundaries Approach)
- API / Data Contracts:
  - Apple Sign In with JavaScript SDK Documentation
  - Apple Sign In with REST API Documentation
  - Apple Key Server for Public Keys
- Policies / Regulations:
  - Apple Sign In with Apple Review Guidelines
  - Apple Developer Program License Agreement
- Design Artifacts:
  - ccef-ui-ux/prototype/index.html (SSO button implementation and flow)
- Other:
  - Apple Sign In with Apple Developer Documentation
  - Apple Human Interface Guidelines for Sign In with Apple

## Traceability
Planning objects this requirement supports or constrains.

- Product Slices:
  - PS-CCEF-001
- Use Cases:
  - UC-CCEF-001

Traceability rules:
- Every Requirement not marked Out of Scope must trace to at least one Product Slice.
- Every functional Requirement not marked Out of Scope must trace to at least one Use Case not marked Out of Scope or approved Product Slice objective.
- Every Use Case not marked Out of Scope must be covered by one or more functional Requirements not marked Out of Scope before implementation begins.
- Cross-cutting Requirements not marked Out of Scope may trace directly to the Product Slice when Use Case linkage would be artificial.
- Out of Scope Use Cases and Requirements are excluded from active traceability, coverage, and consistency checks. Links to or from Out of Scope artifacts may remain as historical/contextual references, but must not satisfy active implementation gates.
- Implementation work not covered by an approved Requirement is speculative and should be surfaced as a planning gap or marked as over-engineering.