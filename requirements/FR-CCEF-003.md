# Requirement

- Requirement ID: FR-CCEF-003
- Title: Support Email One-Time Code Authentication
- Requirement Type: functional
- Product Slice IDs: PS-CCEF-001
- Lifecycle State: Approved

## Requirement Statement
The system shall support account creation and sign-in using a one-time code delivered via email as a fallback authentication method.

## Rationale
Providing an email one-time code fallback ensures users can access their accounts even when SSO providers are unavailable or when they prefer not to use social login. This increases reliability and provides choice in authentication methods while maintaining security through time-limited, single-use codes.

## Acceptance Criteria
- Given a user on the account creation or sign-in page
- When the user chooses the email authentication method (either "Create account" or "Email me a sign-in code")
- And the user provides a valid email address
- Then the system shall generate a cryptographically secure 6-digit one-time code using an approved CSPRNG
- And the system shall send the one-time code to the provided email address via a secure email service (TLS encrypted)
- And the system shall store a salted hash of the code using bcrypt with appropriate cost factor
- And the system shall store the expiration timestamp (current time + 10 minutes) alongside the hashed code
- And the system shall present a code input interface with 6 separate input fields for better UX
- And when the user enters the correct 6-digit code within the expiration window
- Then the system shall validate the code using constant-time comparison to prevent timing attacks
- And if validating for account creation, the system shall create a new user account with the provided email
- And if validating for sign-in, the system shall authenticate the existing user associated with the email
- And the system shall establish an authenticated session for the user with appropriate session identifier
- And the system shall redirect the user to the post-authentication flow (onboarding or main app) within 2 seconds (±200ms tolerance)
- And the system shall invalidate the used one-time code immediately after successful validation
- And the system shall handle expired codes gracefully by requesting a new code (with user feedback)
- And the system shall rate-limit code generation to maximum 3 requests per email address per hour
- And the system shall provide clear feedback when attempting to resend a code too soon
- And the system shall handle email delivery failures by informing the user and allowing retry
- And the system shall not reveal whether an email address is registered through timing or error messages

## Explicit Exclusions
- Password creation or management (the system does not use or store passwords)
- Manual email verification links or clicks (the system uses code entry, not link clicking)
- Custom code lengths or formats (fixed at 6 digits for consistency)
- Internationalization of the code input interface (covered by separate requirements)
- Email delivery failure handling beyond basic retry mechanisms
- Support for alternative email providers or custom SMTP configurations
- Integration with enterprise email systems or SSO gateways
- Long-term code storage or code reuse capabilities

## Constraints
- Must use cryptographically secure random number generation for code creation
- Must store only a hashed version of the code (never the plaintext code)
- Must use a strong, slow hashing algorithm appropriate for secrets (bcrypt, scrypt, or PBKDF2)
- Must enforce a 10-minute expiration window for all one-time codes
- Must implement rate limiting on code generation per email address and IP address
- Must use a secure email delivery service with proper authentication and TLS encryption
- Must validate email format before attempting to send a code
- Must handle email delivery failures gracefully with user feedback and retry options
- Must clear expired codes from storage periodically to prevent accumulation
- Must not leak timing information during code validation to prevent side-channel attacks
- Must ensure code input fields are not susceptible to autocomplete or prediction attacks

## Validation Method
- Automated test: Unit tests for code generation, hashing, and validation logic
- Automated test: Integration tests simulating email delivery and code verification
- Manual QA: End-to-end testing with actual email delivery (using test email service)
- Security review: Validation of cryptographic storage and timing attack resistance
- Architecture review: Confirmation of proper separation between auth and email services
- Performance testing: Verification of rate limiting under load
- Compliance review: Verification of alignment with NIST guidelines for OOB authentication

## References
Approved artifacts this requirement should be interpreted with.

- Related Requirements, non-blocking:
  - FR-CCEF-001 (Google SSO support)
  - FR-CCEF-002 (Apple SSO support)
  - FR-CCEF-004 (Account linking/unlinking)
  - FR-CCEF-005 (Email format validation)
- ADRs:
  - ADR-0001 (Modular Monolith with Clear Boundaries Approach)
- API / Data Contracts:
  - RFC 4086 (Randomness Requirements for Security)
  - NIST SP 800-63B (Digital Identity Guidelines)
- Policies / Regulations:
  - NIST Special Publication 800-63B: Authentication and Lifecycle Management
  - OWASP Authentication Cheat Sheet
  - ISO/IEC 29115:2013 Entity authentication assurance framework
- Design Artifacts:
  - ccef-ui-ux/prototype/index.html (Email one-time code implementation)
- Other:
  - Google reCAPTCHA or equivalent for abuse prevention
  - Email service provider documentation (SendGrid, SES, etc.)

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