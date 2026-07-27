# Task

- Task ID: TASK-MS-CCEF-001-003
- Milestone ID: MS-CCEF-001
- Title: Implement email OTP generation, validation, and rate-limiting
- Lifecycle State: Approved

## Dependencies
- Predecessor Task: TASK-MS-CCEF-001-002
- Included Requirement IDs: FR-CCEF-001, FR-CCEF-002, FR-CCEF-003, FR-CCEF-004, FR-CCEF-005, FR-CCEF-006, FR-CCEF-007, FR-CCEF-009, FR-CCEF-015, NFR-CCEF-001, NFR-CCEF-002, NFR-CCEF-003, NFR-CCEF-004, NFR-CCEF-005, NFR-CCEF-006, NFR-CCEF-007

## Task scope
- Scope:
  - Secure OTP generation using cryptographically secure random values
  - OTP validation logic (correctness and expiration)
  - Rate limiting implementation for OTP generation requests
  - Unit testing of OTP generation, validation, expiration, and one-time use
  - Integration testing of email OTP flow
  - Brute-force and replay attack resistance mechanisms
  - User-facing code input interface with 6 separate fields for OTP entry
  - User-facing error messages for invalid/expired OTP codes
  - User-facing retry-after feedback when rate-limited
  - Preservation of entered email and OTP state on failure (network or validation error)
  - GDPR-compliant privacy notice implementation and display before OTP submission
  - Explicit user consent capture workflow for email usage in OTP flow
- Non-Scope:
  - Email delivery service implementation (uses external service)
  - SSO token validation (covered in SSO validation task)
  - User account creation logic (covered in account creation task)
  - Consent capture mechanisms (covered in GDPR task)

## Traceability
- Requirement IDs: FR-CCEF-001, FR-CCEF-002, FR-CCEF-003, FR-CCEF-004, FR-CCEF-005, FR-CCEF-006, FR-CCEF-007, FR-CCEF-009, FR-CCEF-015, NFR-CCEF-001, NFR-CCEF-002, NFR-CCEF-003, NFR-CCEF-004, NFR-CCEF-005, NFR-CCEF-006, NFR-CCEF-007
- Use Cases: UC-CCEF-001, UC-CCEF-003
- Scope:
  - Secure OTP generation using cryptographically secure random values
  - OTP validation logic (correctness and expiration)
  - Rate limiting implementation for OTP generation requests
  - Unit testing of OTP generation, validation, expiration, and one-time use
  - Integration testing of email OTP flow
  - Brute-force and replay attack resistance mechanisms
  - User-facing code input interface with 6 separate fields for OTP entry
  - User-facing error messages for invalid/expired OTP codes
  - User-facing retry-after feedback when rate-limited
  - Preservation of entered email and OTP state on failure (network or validation error)
  - GDPR-compliant privacy notice implementation and display before OTP submission
  - Explicit user consent capture workflow for email usage in OTP flow
- Non-Scope:
  - Email delivery service implementation (uses external service)
  - SSO token validation (covered in SSO validation task)
  - User account creation logic (covered in account creation task)
  - Consent capture mechanisms (covered in GDPR task)
- Completion Criteria:
  - Secure OTP generation implemented with cryptographically secure random values
  - OTP validation logic implemented (correctness and expiration checks)
  - Rate limiting implemented on OTP generation to prevent abuse
  - Unit tests cover OTP generation, validation, expiration, and one-time use
  - Integration tests verify email OTP flow with simulated email service
  - Brute-force and replay attack resistance verified
  - Code input interface with 6 separate fields implemented and tested
  - User-facing error messages for invalid/expired OTP codes displayed appropriately
  - Retry-after feedback (e.g., 'Please wait 60 seconds before requesting a new code') shown when rate-limited
  - Entered email and OTP state preserved on failure (network error, invalid code, etc.)
  - GDPR-compliant privacy notice implemented and displayed before OTP submission
  - Explicit user consent capture workflow implemented for email usage in OTP flow

## Architecture and quality
- Required ADR IDs: ADR-0001, ADR-0002, ADR-0003
- Quality Gates:
  - Email OTP flow must resist brute-force and replay attacks
  - Response times for authentication must meet benchmarks: SSO < 800ms, OTP < 500ms
  - System enforces rate limiting on code generation to prevent abuse
- QA Obligations:
  - Email OTP flow must resist brute-force and replay attacks – implement and test rate‑limiting, nonce usage, and expiration checks
  - System enforces rate‑limiting on OTP generation and shows appropriate feedback when limit is reached
  - Invalid or expired Google ID token should be rejected and logged
  - Invalid or expired Apple identity token should be rejected and logged
  - Expired or reused one‑time code must be rejected
  - Brute‑force attempts against OTP endpoint must be throttled and flagged
  - Replay attacks on OTP must be prevented

## Lane planning guidance
- Expected Lane Involvement: backend, api, frontend
- Lane Boundary Notes:
  - Task involves backend and API lanes; later work items must split implementation into one lane each while maintaining API contract consistency
