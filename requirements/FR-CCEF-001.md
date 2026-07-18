# Requirement

- Requirement ID: FR-CCEF-001
- Title: Support Google SSO Account Creation
- Requirement Type: functional
- Product Slice IDs: PS-CCEF-001
- Lifecycle State: Approved

## Requirement Statement
The system shall support account creation via Google Single Sign-On (SSO) provider.

## Rationale
Users should be able to create accounts using their existing Google identity for convenience and security, eliminating the need to manage separate passwords. This aligns with modern authentication practices and reduces friction in the onboarding process.

## Acceptance Criteria
- Given a user on the account creation or sign-in page
- When the user clicks the "Continue with Google" button
- Then the system shall redirect the user to Google's authentication service using OAuth 2.0/OIDC compliant flow
- And after successful Google authentication, the system shall receive an authorization code from Google
- And the system shall exchange the authorization code for an ID token and access token using Google's token endpoint
- And the system shall validate the ID token signature, expiration, audience, and issuer claims using Google's public keys
- And the system shall validate the nonce parameter to prevent replay attacks
- And the system shall validate that the redirect_uri matches a pre-registered value to prevent open redirect attacks
- And the system shall extract the user's email, given_name, and family_name from the validated ID token
- And the system shall normalize the email address to lowercase for account lookup
- And the system shall check if a user account already exists for the Google account (by email or sub claim)
- And if no account exists, the system shall create a new user account linked to the Google identity
- And if an account exists, the system shall authenticate the existing user (if not already authenticated)
- And the system shall establish an authenticated session for the user with appropriate session identifier
- And the system shall create a new session identifier after login to prevent session fixation
- And the system shall set secure session cookie attributes (HttpOnly, Secure, SameSite=Strict)
- And the system shall redirect the user to the post-authentication flow (onboarding or main app) within 2 seconds (±200ms tolerance)
- And the system shall clear any transient authentication state after successful completion
- And the system shall handle the case where the user denies the permission request from Google by displaying the exact message "Authentication was cancelled – please try again" within 500ms and logging event code AUTH_DENIED
- And the system shall handle network failures or timeouts during the Google authentication flow by displaying the exact message "Network error – please try again later" within 500ms and logging the event with timeout duration and event code AUTH_NETWORK_ERROR
- And the system shall present a GDPR-compliant privacy notice in a modal dialog requiring an explicit "I agree" checkbox action before proceeding, and shall record the checkbox state, timestamp, and notice version
- And the system shall obtain and record explicit user consent for processing personal data (email, name) through an explicit opt-in action (checkbox selection) and shall store the consent timestamp, version, and user's consent decision
- And the system shall store consent timestamp and version for audit purposes
- And the system shall encrypt audit log entries containing PII with AES-256-GCM
- And the system shall include a SHA-256 hash of PII fields in audit logs for verification

## Explicit Exclusions
- Password creation or management for Google SSO accounts (handled by Google)
- Manual email verification for Google SSO accounts (email verification is handled by Google)
- Collection of additional profile information beyond email and basic name during SSO flow
- Support for Google Workspace domain restrictions or enterprise-specific features
- Handling of re-authentication requests or session renewal (covered by separate requirements)

## Constraints
- Must use OAuth 2.0 and OpenID Connect standards for Google SSO integration
- Must validate ID tokens using Google's published JSON Web Key Set (JWKS)
- Must reject tokens with invalid signatures, expired timestamps, or incorrect audience
- Must use HTTPS for all communications with Google's authentication endpoints
- Must store OAuth state parameter to prevent CSRF attacks during the flow
- Must implement PKCE (Proof Key for Code Exchange) for public client security
- Must validate the nonce parameter to prevent replay attacks (OIDC Core)
- Must validate redirect_uri against a pre-registered whitelist to prevent open redirect attacks
- Must enforce Content Security Policy headers
- Must enforce X-Frame-Options to prevent clickjacking
- Must enforce TLS version 1.2 or higher for all provider communications
- Must not store Google access tokens longer than necessary for the authentication flow
- Must retrieve user profile information using the access token via Google's userinfo endpoint
- Must link the SSO account to a single CCEF user account (no account merging/splitting in this flow)
- Must store user profile data (email, name) in compliance with GDPR data minimization principles
- Must retain user profile data only as long as necessary for account functionality
- Must implement pseudonymization of audit logs containing PII
- Must maintain records of processing activities for personal data (GDPR Art. 30)
- Must conduct Data Protection Impact Assessment for SSO authentication flows
- Must implement breach detection and notification procedures (GDPR Art. 33-34)
- Must ensure cross-border data transfers comply with GDPR Chapter V (SCCs/DPAs)
- Must apply privacy-by-design and privacy-by-default principles

## Validation Method
- Automated test: Unit tests for token validation logic
- Automated test: Integration tests simulating the complete Google SSO flow
- Manual QA: End-to-end testing with actual Google developer project
- Security review: Validation of token handling and cryptographic validation
- Architecture review: Confirmation of proper separation of concerns in auth implementation

## References
Approved artifacts this requirement should be interpreted with.

- Related Requirements, non-blocking:
  - FR-CCEF-002 (Apple SSO support)
  - FR-CCEF-003 (Email one-time code fallback)
  - FR-CCEF-004 (Account linking/unlinking)
- ADRs:
  - ADR-0001 (Modular Monolith with Clear Boundaries Approach)
- API / Data Contracts:
  - Google OpenID Connect Discovery Document
  - Google Token Endpoint Specification
  - Google UserInfo Endpoint Specification
- Policies / Regulations:
  - OAuth 2.0 Threat Model and Security Considerations (RFC 6819)
  - OpenID Connect Core 1.0
- Design Artifacts:
  - ccef-ui-ux/prototype/index.html (SSO button implementation and flow)
- Other:
  - Google OAuth 2.0 Implementation Guidelines

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