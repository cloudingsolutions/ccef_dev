# Milestone

- Milestone ID: MS-CCEF-003
- Product Slice ID: PS-CCEF-001
- Title: Data Residency Confirmation
- Lifecycle State: Ready for Approval

## Objective

Enable users to confirm or select their data residency region during onboarding, with system inference from IP address (Europe as minimum) and manual selection where legally permitted, ensuring GDPR compliance and transparent data handling.

## Dependencies

- Predecessor Milestones: MS-CCEF-002
- Included Requirement IDs: FR-CCEF-032

## Explicit Exclusions

- UC-CCEF-002 (Out of Scope - covered in UC-CCEF-001 for both Google and Apple SSO)
- FR-CCEF-008, FR-CCEF-010, FR-CCEF-011, FR-CCEF-012, FR-CCEF-013, FR-CCEF-014, FR-CCEF-016, FR-CCEF-017 (Out of Scope functional requirements)
- UC-CCEF-009 and beyond (if any exist)
- Deferred / adjacent product intent: organization/team management, complex authorization schemes, additional languages beyond English/Swedish, advanced account recovery, social login beyond Google/Apple, advanced privacy controls, data export, data retention policies, account closure, subscription management, API access, multi-currency, role-based views, audit logging for compliance, data residency beyond Europe, additional privacy frameworks, onboarding flows beyond account creation, product tours, in-app messaging, log aggregation, API rate limiting, multi-tenant architecture, data partitioning, accessibility enhancements beyond WCAG 2.2 AA, internationalization frameworks.
- Automatic residency changes based on detected location changes after initial setup
- Requiring residency selection to complete initial account creation (explicitly excluded per UC-CCEF-008)
- Ability to change residency after initial onboarding completion
- Residency-based feature flags or conditional functionality
- Data partitioning or sharding based on residency
- Legal advice or interpretation of residency regulations
- Integration with external residency verification services
- Residency confirmation via government ID or documentation
- Phone number verification and SMS consent setup (covered in Milestone 2)
- Account settings for updating name, language, and contact preferences (covered in Milestone 4)
- Language selection and legal acceptance (covered in Milestone 1)

## Traceability

- Included Use Case IDs: UC-CCEF-008
- Architectural Assumptions:
  - The system follows a modular monolith approach with clear boundaries as defined in ADR-0001.
  - GDPR-compliant data handling practices are implemented as specified in ADR-0002, including data residency controls and constraints.
  - The system uses a geolocation service or IP-to-location mapping for residency inference, with configurable confidence thresholds.
  - Supported residency regions are configurable based on legal and regulatory considerations, with Europe as minimum.
  - Data storage locations are mapped to residency regions, with actual data routing handled at the infrastructure level.
  - The system uses a separate privacy module for managing residency records and consent as outlined in ADR-0002.
  - Residency data is stored as part of the user profile or in a dedicated privacy data store.
  - Audit logging captures residency determination events for compliance and security monitoring.
  - The system does not implement automatic residency updates based on location changes to ensure stability and compliance.
  - Residency confirmation occurs during onboarding but is not required to complete initial account creation (per UC-CCEF-008 Explicit Exclusions).
  - The system maintains separation between residency data and other personal data for clear auditability.
- Required ADRs: ADR-0001, ADR-0002
- Quality Gates:
  - Code review by system architect and privacy/compliance specialist
  - Unit test coverage ≥ 90% for new functionality
  - Integration tests covering IP inference, region validation, and selection flows
  - End-to-end test scenarios for residency confirmation process
  - Privacy and compliance review verifying GDPR adherence for data residency handling and transparency
  - Security review focusing on geolocation service integration and data protection
  - Performance testing for residency inference under load
  - Accessibility testing (WCAG 2.2 AA) for region selection interface
  - User acceptance testing with representative users for residency confirmation and understanding of data residency implications
- Demo Criteria:
  - Demonstrate residency inference: simulate IP address from a European country, observe system pre-selecting European region during onboarding.
  - Demonstrate residency inference failure: simulate IP address from unsupported region, observe system prompting for manual region selection.
  - Demonstrate region selection: choose a supported non-European region (where legally permitted) and see confirmation.
  - Demonstrate inferred vs. user-selected distinction: check that UI and records clearly show whether residency was inferred or user-selected.
  - Demonstrate unsupported region prevention: attempt to select an unsupported region and see clear explanation why it's not available.
  - Demonstrate audit trail recording: verify that residency determination attempts and outcomes are recorded in audit trail (via admin interface or logs).
  - Demonstrate residency display in account settings: navigate to account settings after onboarding and view recorded residency (display-only).
  - Demonstrate edge case handling: simulate VPN/proxy usage, observe system prompting for manual selection due to lowered inference confidence.
  - Demonstrate no silent assignment: confirm that system never assigns arbitrary region when inference fails; always requires user selection.
  - Demonstrate explanation display: view explanation of what data residency means for the user during onboarding and in account settings.
- Acceptance Criteria:
  - System attempts to infer user's data residency region from IP address using a geolocation service.
  - When inference is confident and region is supported (Europe or other legally permitted regions), system pre-selects that region during onboarding.
  - When inference fails or region is unsupported, system prompts user to select region from a list of supported regions.
  - Europe is presented as the minimum supported residency region during the selection process.
  - Users can select another supported region where regulation permits choice (based on current legal considerations).
  - System clearly indicates when residency is inferred vs. user-selected in the UI and in stored records.
  - System prevents selection of unsupported regions with clear explanation why the region is not available.
  - System does not silently assign users to arbitrary regions when residency cannot be determined; instead, it requires manual selection.
  - Selected or inferred residency is recorded with timestamp and user ID in the user profile or privacy module.
  - System provides explanation of what data residency means for the user (e.g., where their data is stored, applicable regulations).
  - User can view their recorded residency in account settings (display-only, not changeable after onboarding).
  - System handles edge cases like VPNs, proxies, and mobile roaming appropriately by lowering inference confidence and prompting for manual selection.
  - Residency determination attempts and outcomes (success, failure, user selection) are recorded in the audit trail for compliance.
  - If the inferred region is unsupported, system explains why the region is not available and requires user to select a supported region.
  - If residency cannot be confidently inferred, system presents manual selection interface without silently assigning an arbitrary region.
  - System does not automatically change residency based on detected location changes after initial setup.
  - Residency-based feature flags or conditional functionality are not implemented in this slice.
  - Data partitioning or sharding based on residency is not implemented in this slice.

## Release Branches

1. Release branch creation happens only after Human green-light.

## Artifacts

- Completion Evidence: None.

### Coverage Matrix

| Requirement ID | Covered In This Milestone? | Fully/Partially Covered | Validation Method |
|---|---|---|---|
| FR-CCEF-032 | True | Full | Unit tests for IP-based residency inference, integration tests with mock geolocation service, end-to-end test scenarios for residency confirmation flow. |

### Increment Integrity

- Can this milestone be demoed independently? Yes.
- Can this milestone be deployed safely? Yes.
- What feature flags or disabled paths are required? Automatic residency updates based on location changes are disabled/not available; residency-based feature flags are disabled/not available; data partitioning/sharding by residency is disabled/not available.
- What user-visible behavior is intentionally incomplete? Users cannot change their data residency region after initial onboarding completion; the system does not automatically update residency based on detected location changes; residency-based feature flags or conditional functionality are not available; data partitioning or sharding based on residency is not implemented.
