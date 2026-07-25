# Use Case

- Use Case ID: UC-CCEF-001
- Title: User creates an account with Google or Apple SSO
- Product Slice IDs: PS-CCEF-001
- Lifecycle State: Approved

## Summary
A user can create an account using Google or Apple Single Sign-On (SSO) providers, which provides a secure and convenient authentication method without requiring password management.

## Actor
Potential user visiting the CCEF website for the first time

## Trigger
User clicks on "Continue with Google" or "Continue with Apple" button on the landing page or sign-in page

## Outcome
User successfully creates an account and is authenticated into the system, with their account linked to their Google or Apple identity

## Success Criteria
1. User is redirected to the respective provider's authentication page
2. User successfully authenticates with their Google or Apple account
3. User is redirected back to CCEF with a valid authentication token
4. System creates a new user account linked to the provider account
5. User is authenticated and redirected to the post-onboarding flow
6. User's basic profile information (name, email) is populated from the provider
7. Account is created with compliant onboarding defaults applied
8. User receives a success message indicating account creation was successful
9. An audit log entry is created for the SSO sign-up attempt
10. Explicit user consent is obtained and recorded before processing personal data (email, name)
11. A GDPR-compliant privacy notice is presented before collecting personal data
12. If the user cancels provider authentication, the system shows a user-facing cancellation message and lets the user retry or choose another authentication method
13. If the provider callback, token validation, or network redirect fails, the system shows a user-facing error message and lets the user retry without creating a partial account
14. If the user is temporarily rate limited, the system shows a user-facing retry-after message without revealing account existence

## Explicit Exclusions
- Password creation or management for SSO accounts
- Manual email verification for SSO accounts (handled by provider)
- Requiring phone number collection to complete SSO account creation; optional post-account phone setup is covered by UC-CCEF-004
- Requiring language preference selection to complete SSO account creation; language selection during onboarding and settings is covered by UC-CCEF-005 and UC-CCEF-006

## Linked Requirement IDs
- FR-CCEF-001
- FR-CCEF-002
- FR-CCEF-003
- FR-CCEF-004
- FR-CCEF-005
- FR-CCEF-006
- FR-CCEF-007
- NFR-CCEF-001
- NFR-CCEF-002
- NFR-CCEF-003
- NFR-CCEF-004
- NFR-CCEF-005
- NFR-CCEF-006
- NFR-CCEF-007
