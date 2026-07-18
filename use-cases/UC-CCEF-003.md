# Use Case

- Use Case ID: UC-CCEF-003
- Title: User creates an account with email and one-time code
- Product Slice IDs: PS-CCEF-001
- Lifecycle State: Approved

## Summary
A user can create an account using email and a one-time code sent to their email address, providing a passwordless authentication option that still verifies email accessibility.

## Actor
Potential user visiting the CCEF website for the first time who prefers passwordless authentication

## Trigger
User submits their email address on the sign-up page to request a one-time code

## Outcome
User successfully creates an account using the one-time code and is authenticated into the system

## Success Criteria
1. System validates email format and checks that email is not already registered
2. System generates and sends a secure one-time code to the user's email
3. User receives the one-time code email and enters it into the verification form
4. System validates the one-time code is correct and not expired
5. System creates a new user account for verified email
6. User is authenticated and redirected to complete the onboarding flow
7. User can log in using email and one-time code for future sessions
8. System enforces rate limiting on code generation to prevent abuse
9. Account is created with compliant onboarding defaults applied
10. User receives clear feedback about code expiration and resend options

## Explicit Exclusions
- Password creation or management for this authentication method
- Social Sign-On options (Google/Apple) for this flow
- Phone number collection during initial registration (handled in separate flow)
- Language preference setting during initial registration (handled in post-onboarding)
- Code reuse prevention (each code can only be used once)

## Linked Requirement IDs
FR-CCEF-003
FR-CCEF-006
FR-CCEF-007
FR-CCEF-009
FR-CCEF-011
FR-CCEF-012
FR-CCEF-015
NFR-CCEF-001
NFR-CCEF-002
NFR-CCEF-003
NFR-CCEF-004
NFR-CCEF-005
NFR-CCEF-006