# Use Case

- Use Case ID: UC-CCEF-007
- Title: User views and accepts terms & conditions and privacy policy
- Product Slice IDs: PS-CCEF-001
- Lifecycle State: Approved

## Summary
During the onboarding flow, users are presented with and must accept the terms & conditions and privacy policy before completing account creation, ensuring legal compliance and informed consent.

## Actor
User completing the account creation process who has not yet accepted legal agreements

## Trigger
User reaches the legal agreements step in the onboarding flow after providing account information

## Outcome
User has viewed and explicitly accepted both the terms & conditions and privacy policy, allowing account creation to proceed

## Success Criteria
1. System presents clear, readable versions of both terms & conditions and privacy policy
2. Documents are presented in the user's selected language (English or Swedish)
3. User must scroll to the bottom of each document to enable the acceptance checkbox
4. Acceptance checkboxes are not pre-checked, requiring explicit user action
5. User can select to view either document independently
6. System records acceptance of both documents with timestamp and user ID
7. User cannot proceed with account creation without accepting both documents
8. System provides links to view the full documents in a modal or new page
9. Acceptance is stored durably and can be retrieved for audit purposes
10. System indicates which specific version of each document was accepted
11. User receives clear confirmation that legal agreements have been accepted
12. Links to the documents are accessible from account settings for future reference
13. Acceptance actions are recorded in the audit trail for compliance purposes

## Explicit Exclusions
- Ability to modify or negotiate terms of service
- Version history or diff views of legal documents
- Electronic signature capture beyond checkbox acceptance
- Language options beyond English and Swedish for legal documents
- Print-friendly or downloadable versions of the documents
- Multilingual support for the legal documents themselves
- A/B testing or variation of legal document presentation
- Caching of legal documents for extended periods (must check for updates)

## Linked Requirement IDs
- FR-CCEF-031
- NFR-CCEF-009