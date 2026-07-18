# Use Case

- Use Case ID: UC-CCEF-002
- Title: User creates an account with email and password
- Product Slice IDs:
- Lifecycle State: Out of Scope

## Summary
A user can create an account using traditional email and password authentication, which requires email verification to ensure the email address is valid and accessible to the user.

## Actor
Potential user visiting the CCEF website for the first time who prefers email/password authentication

## Trigger
User submits the registration form with email address and password on the sign-up page

## Outcome
User successfully creates an account, verifies their email address, and is authenticated into the system

## Success Criteria
1. System validates email format and password strength requirements
2. System checks that the email address is not already registered
3. System creates a new user account with hashed password storage
4. System sends a verification email to the provided email address
5. User clicks the verification link in the email
6. System confirms email verification and activates the account
7. User is redirected to complete the onboarding flow
8. User can log in with their email and password after verification
9. Account is created with compliant onboarding defaults applied
10. User receives appropriate feedback at each step of the process
11. Password change requires re-authentication for security-sensitive operations

## Explicit Exclusions
- Social Sign-On options (Google/Apple) for this flow
- Phone number collection during initial registration (handled in separate flow)
- Password recovery/reset functionality (deferred to later slice)
- Language preference setting during initial registration (handled in post-onboarding)

## Linked Requirement IDs
FR-CCEF-005
FR-CCEF-006
FR-CCEF-007
FR-CCEF-008
FR-CCEF-009
FR-CCEF-010
FR-CCEF-011
FR-CCEF-012
FR-CCEF-013
FR-CCEF-014
FR-CCEF-015
FR-CCEF-016
FR-CCEF-017
NFR-CCEF-001
NFR-CCEF-002
NFR-CCEF-003
NFR-CCEF-004
NFR-CCEF-005
NFR-CCEF-006