# Requirement

- Requirement ID: FR-CCEF-020
- Title: SMS Consent Capture and Recording for GDPR Compliance
- Requirement Type: functional
- Product Slice IDs: PS-CCEF-001
- Lifecycle State: Approved

## Requirement Statement
The system shall capture and record explicit user consent for SMS communications in compliance with GDPR and telecommunications regulations.

## Rationale
Explicit consent is required under GDPR and telecommunications regulations (such as TCPA) for sending commercial SMS messages. Proper consent capture ensures legal compliance, builds user trust, and provides an auditable trail for regulatory purposes. The consent must be freely given, specific, informed, and unambiguous.

## Acceptance Criteria
- Given a user has successfully verified their phone number
- When the system presents the SMS consent request
- Then the system shall present a clear, unchecked checkbox for SMS consent (not pre-checked)
- And the system shall provide clear information about what the user is consenting to receive
- And the system shall require explicit action (checkbox selection) to grant consent
- And the system shall not proceed with SMS functionality without explicit consent
- And the system shall record the consent decision with timestamp, user ID, and consent version
- And the system shall store consent records in an immutable audit trail for compliance purposes
- And the system shall encrypt consent records containing PII using AES-256-GCM
- And the system shall include a SHA-256 hash of consent-related PII in audit logs for verification
- And the system shall allow users to withdraw consent at any time through account settings
- And the system shall immediately halt SMS communications upon consent withdrawal
- And the system shall record consent withdrawal with timestamp and reason
- And the system shall provide clear confirmation when consent is granted or withdrawn
- And the system shall maintain consent records for the duration required by applicable regulations

## Explicit Exclusions
- Implied consent or opt-out mechanisms for SMS communications
- Pre-checked consent boxes or default opt-in
- Consent bundled with other terms or conditions
- Consent for non-SMS communications (email, push notifications, etc.)
- Retroactive consent application to previously collected phone numbers
- Alternative verification methods for consent capture

## Constraints
- Must require explicit opt-in action for SMS consent (unchecked checkbox by default)
- Must provide clear, granular consent scope (specifically for SMS alerts)
- Must record consent with timestamp, user ID, and consent version/documentation
- Must store consent records in compliance with GDPR Article 30 (Records of processing activities)
- Must implement pseudonymization or encryption of consent records containing PII
- Must allow easy withdrawal of consent at any time
- Must not use dark patterns or misleading language to obtain consent
- Must comply with GDPR Article 7 (Conditions for consent)
- Must comply with telecommunications regulations regarding consent requirements
- Must maintain consent records for the applicable statute of limitations
- Must provide access to consent records upon user request (GDPR Article 15)
- Must allow users to challenge or correct consent records (GDPR Article 16)

## Validation Method
- Automated test: Unit tests for consent capture and recording logic
- Automated test: Integration tests for consent flow and withdrawal
- Manual QA: Testing consent capture, storage, and withdrawal scenarios
- Security review: Validation of consent data encryption and protection
- Architecture review: Confirmation of proper consent data handling and storage
- Compliance review: Validation of GDPR and telecommunications compliance
- Privacy review: Assessment of consent mechanisms against privacy best practices

## References
Approved artifacts this requirement should be interpreted with.

- Related Requirements, non-blocking:
  - FR-CCEF-018 (Phone Number Input and Validation for Verification)
  - FR-CCEF-019 (SMS Verification Code Generation and Validation)
  - FR-CCEF-021 (Phone Number Management in Account Settings)
- ADRs:
  - ADR-0001 (Modular Monolith with Clear Boundaries Approach)
- API / Data Contracts:
  - GDPR-compliant audit log specifications
  - Selected consent management framework specifications
- Policies / Regulations:
  - GDPR Article 6(1)(a) (Lawfulness of processing - consent)
  - GDPR Article 7 (Conditions for consent)
  - GDPR Article 13 (Information to be provided where personal data are collected)
  - GDPR Article 15 (Right of access by the data subject)
  - GDPR Article 16 (Right to rectification)
  - GDPR Article 17 (Right to erasure/'right to be forgotten')
  - TCPA (Telephone Consumer Protection Act)
  - ePrivacy Directive (where applicable)
- Design Artifacts:
  - ccef-ui-ux/prototype/index.html (SMS consent implementation)
- Other:
  - ISO 27701 (Privacy Information Management)
  - ICO GDPR Consent Guidelines
  - WP29 Guidelines on Consent under Regulation 2016/679

## Traceability
Planning objects this requirement supports or constrains.

- Product Slices:
  - PS-CCEF-001
- Use Cases:
  - UC-CCEF-004

Traceability rules:
- Every Requirement not marked Out of Scope must trace to at least one Product Slice.
- Every functional Requirement not marked Out of Scope must trace to at least one Use Case not marked Out of Scope or approved Product Slice objective.
- Every Use Case not marked Out of Scope must be covered by one or more functional Requirements not marked Out of Scope before implementation begins.
- Cross-cutting Requirements not marked Out of Scope may trace directly to the Product Slice when Use Case linkage would be artificial.
- Out of Scope Use Cases and Requirements are excluded from active traceability, coverage, and consistency checks. Links to or from Out of Scope artifacts may remain as historical/contextual references, but must not satisfy active implementation gates.
- Implementation work not covered by an approved Requirement is speculative and should be surfaced as a planning gap or marked as over-engineering.