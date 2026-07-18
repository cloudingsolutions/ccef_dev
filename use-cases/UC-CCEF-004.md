# Use Case

- Use Case ID: UC-CCEF-004
- Title: User provides and verifies phone number for SMS consent
- Product Slice IDs: PS-CCEF-001
- Lifecycle State: Approved

## Summary
After account creation, users provide and verify their phone number to enable SMS alert functionality, with explicit consent captured for GDPR compliance.

## Actor
Registered user who has completed account creation but not yet verified phone number

## Trigger
User navigates to phone verification step in onboarding flow or accesses phone settings in account management

## Outcome
User's phone number is verified and explicit consent is captured for SMS communications

## Success Criteria
1. User enters their phone number in the correct international format
2. System validates phone number format and checks if already associated with another account
3. System sends a one-time verification code via SMS to the provided number
4. User receives the SMS and enters the verification code
5. System validates the code is correct and not expired
6. System marks the phone number as verified for the user's account
7. System presents a clear consent request for SMS alerts
8. User explicitly opts in to receive SMS alerts (not pre-checked)
9. System records the consent with timestamp and user ID for audit purposes
10. User receives confirmation that phone verification and consent are complete
11. System enforces rate limiting on SMS code generation to prevent abuse
12. User can update or remove their phone number in account settings with appropriate consent handling
13. Consent actions are recorded in the audit trail for compliance purposes

## Explicit Exclusions
- Phone number collection during initial account creation (separate from verification)
- SMS alert delivery functionality (covered in other use cases)
- Phone number porting or carrier change handling
- International phone number restrictions based on regulatory requirements
- Voice call verification as alternative to SMS

## Linked Requirement IDs
- FR-CCEF-018
- FR-CCEF-019
- FR-CCEF-020
- FR-CCEF-021