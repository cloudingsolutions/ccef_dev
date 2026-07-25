# Use Case

- Use Case ID: UC-CCEF-004
- Title: User provides and verifies phone number for SMS consent
- Product Slice IDs: PS-CCEF-001
- Lifecycle State: Approved

## Summary
After account creation, users may provide and verify their phone number to enable SMS alert functionality, with explicit consent captured for GDPR compliance. Users may skip phone setup and complete it later from account settings.

## Actor
Registered user who has completed account creation and may choose to add, verify, skip, update, or remove a phone number

## Trigger
User navigates to phone verification step in onboarding flow or accesses phone settings in account management

## Outcome
User either skips phone setup, or verifies a phone number and records explicit consent for SMS communications

## Success Criteria
1. User is offered phone setup after account creation without blocking account creation completion
2. User can skip phone setup and continue onboarding without verified phone number or SMS consent
3. If the user chooses phone setup, user enters their phone number in the correct international format
4. System validates phone number format and checks if already associated with another account
5. System sends a one-time verification code via SMS to the provided number
6. User receives the SMS and enters the verification code
7. System validates the code is correct and not expired
8. System marks the phone number as verified for the user's account
9. System presents a clear consent request for SMS alerts
10. User explicitly opts in to receive SMS alerts (not pre-checked)
11. System records the consent with timestamp and user ID for audit purposes
12. User receives confirmation that phone verification and consent are complete
13. System enforces rate limiting on SMS code generation to prevent abuse
14. User can update or remove their phone number in account settings with appropriate consent handling
15. Consent actions are recorded in the audit trail for compliance purposes
16. If SMS delivery, code validation, expiration, or rate limiting prevents completion, the system shows a user-facing error message and recovery action

## Explicit Exclusions
- Requiring phone number collection to complete initial account creation
- SMS alert delivery functionality (covered in other use cases)
- Phone number porting or carrier change handling
- International phone number restrictions based on regulatory requirements
- Voice call verification as alternative to SMS

## Linked Requirement IDs
- FR-CCEF-018
- FR-CCEF-019
- FR-CCEF-020
- FR-CCEF-021
