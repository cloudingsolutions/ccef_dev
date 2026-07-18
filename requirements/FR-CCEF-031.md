# Requirement

- Requirement ID: FR-CCEF-031
- Title: Terms and Conditions and Privacy Policy Acceptance
- Requirement Type: functional
- Product Slice IDs: PS-CCEF-001
- Lifecycle State: Approved

## Requirement Statement
The system shall present clear, readable versions of both the terms & conditions and privacy policy during the account creation flow, require explicit user acceptance of both documents before proceeding, and store acceptance records with timestamps and version information for compliance and audit purposes.

## Rationale
Legal compliance requires that users provide informed consent to the terms of service and privacy policy before using the system. This requirement ensures that users are presented with these legal documents in an accessible format, must explicitly accept them (not pre-checked), and that their acceptance is recorded durably for audit trail purposes. This protects both the user (ensuring informed consent) and the company (providing evidence of compliance).

## Acceptance Criteria
- Given a user is in the account creation flow and has reached the legal agreements step
- When the system presents the terms & conditions and privacy policy
- Then the system shall display clear, readable versions of both documents
- And the documents shall be presented in the user's selected language (English or Swedish)
- And the user must scroll to the bottom of each document to enable the corresponding acceptance checkbox
- And the acceptance checkboxes shall not be pre-checked, requiring explicit user action
- And the user shall be able to view either document independently
- When the user attempts to proceed without accepting both documents
- Then the system shall prevent progression and indicate which documents require acceptance
- When the user accepts both documents by scrolling and checking the boxes
- Then the system shall record acceptance of both documents with timestamp, user ID, and document version
- And the system shall allow the user to proceed with account creation
- And the system shall store the acceptance durably for audit and compliance purposes
- Given a user has accepted the terms & conditions and privacy policy
- When the user views their account settings
- Then the system shall provide links to view the accepted documents
- And the system shall indicate which specific version of each document was accepted
- Given a compliance audit is being performed
- When auditors request proof of user consent
- Then the system shall be able to retrieve acceptance records showing which documents were accepted, when, and by which user

## Explicit Exclusions
- Ability to modify or negotiate terms of service
- Version history or diff views of legal documents
- Electronic signature capture beyond checkbox acceptance
- Language options beyond English and Swedish for legal documents
- Print-friendly or downloadable versions of the documents
- Multilingual support for the legal documents themselves
- A/B testing or variation of legal document presentation
- Caching of legal documents for extended periods (must check for updates)

## Constraints
- Must verify that users have scrolled to the bottom of each document before enabling acceptance
- Must not pre-check acceptance checkboxes
- Must prevent account creation progression until both documents are accepted
- Must store acceptance records with timestamps, user ID, and document version information
- Must provide access to accepted documents from account settings for future reference
- Must record acceptance actions in the audit trail for compliance purposes
- Must support both English and Swedish language versions of the documents
- Must allow users to view either document independently
- Must provide links to view full documents in a modal or new page

## Validation Method
- Automated test: Unit tests for terms & conditions and privacy policy presentation logic
- Automated test: Integration tests verifying scroll-to-bottom requirement for checkbox activation
- Automated test: Integration tests verifying prevention of progression without acceptance
- Automated test: Integration tests verifying proper storage of acceptance records
- Manual QA: End-to-end testing with various language selections (English, Swedish)
- Manual QA: Testing scroll-to-bottom functionality for both documents
- Manual QA: Verification that checkboxes are not pre-checked
- Manual QA: Testing that users can view documents independently
- Security review: Validation of acceptance record storage and protection
- Architecture review: Confirmation of proper separation of concerns in legal consent management
- Compliance review: Verification of adherence to informed consent requirements
- User acceptance testing: Validation of usability and clarity of terms & conditions acceptance flow

## References
Approved artifacts this requirement should be interpreted with.

- Related Requirements, non-blocking:
  - FR-CCEF-001 (Google SSO support)
  - FR-CCEF-002 (Apple SSO support)
  - FR-CCEF-003 (Email one-time code fallback)
  - FR-CCEF-004 (Account linking/unlinking)
  - FR-CCEF-005 (Email+Password account creation)
  - FR-CCEF-006 (User consent management)
  - FR-CCEF-007 (Data subject rights)
- ADRs:
  - ADR-0001 (Modular Monolith with Clear Boundaries Approach)
  - ADR-0002 (GDPR-Compliant Data Handling Approach)
- API / Data Contracts:
  - Legal Consent API Specifications
- Policies / Regulations:
  - GDPR Article 7 (Conditions for consent)
  - GDPR Article 12 (Transparent information, communication and modalities)
  - GDPR Article 13 (Information to be provided where personal data are collected)
  - ePrivacy Directive 2002/58/EC (Privacy and electronic communications)
- Design Artifacts:
  - ccef-ui-ux/terms-privacy-acceptance.html (Terms and conditions acceptance interface)
  - ccef-api/legal-consent-endpoints.yaml (Legal consent API specifications)

## Traceability
Planning objects this requirement supports or constrains.

- Product Slices:
  - PS-CCEF-001
- Use Cases:
  - UC-CCEF-007

Traceability rules:
- Every Requirement not marked Out of Scope must trace to at least one Product Slice.
- Every functional Requirement not marked Out of Scope must trace to at least one Use Case not marked Out of Scope or approved Product Slice objective.
- Every Use Case not marked Out of Scope must be covered by one or more functional Requirements not marked Out of Scope before implementation begins.
- Cross-cutting Requirements not marked Out of Scope may trace directly to the Product Slice when Use Case linkage would be artificial.
- Out of Scope Use Cases and Requirements are excluded from active traceability, coverage, and consistency checks. Links to or from Out of Scope artifacts may remain as historical/contextual references, but must not satisfy active implementation gates.
- Implementation work not covered by an approved Requirement is speculative and should be surfaced as a planning gap or marked as over-engineering.