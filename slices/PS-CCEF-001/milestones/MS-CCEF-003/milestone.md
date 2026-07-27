# Milestone

- Milestone ID: MS-CCEF-003
- Product Slice ID: PS-CCEF-001
- Title: Onboarding Completion - Language, Legal, Residency
- Lifecycle State: Approved

## Objective

Enable users to select their preferred language (English or Swedish) during onboarding, accept legal terms & conditions and privacy policy, and confirm or select their data residency region, completing the GDPR-compliant onboarding flow.

## Dependencies

- Predecessor Milestones: MS-CCEF-001, MS-CCEF-002
- Included Requirement IDs: FR-CCEF-022, FR-CCEF-023, FR-CCEF-031, FR-CCEF-032, NFR-CCEF-008, NFR-CCEF-009

## Explicit Exclusions

- UC-CCEF-002 (phone number verification for initial account creation - explicitly excluded)
- FR-CCEF-008 (password strength requirements - explicitly excluded)
- FR-CCEF-010, FR-CCEF-011, FR-CCEF-012, FR-CCEF-013, FR-CCEF-014, FR-CCEF-016, FR-CCEF-017 (various excluded functional requirements)
- Deferred / adjacent product intent: organization/team management, complex authorization schemes, advanced account recovery, social logins beyond Google/Apple, advanced privacy controls, data export, data retention policies, account closure, subscription management, API access, multi-currency, role-based views, audit logging beyond basics, data residency beyond Europe, additional privacy frameworks, onboarding tours, in-app messaging, log aggregation, API rate limiting beyond basics, multi-tenant architecture, data partitioning, accessibility enhancements beyond WCAG 2.2 AA, internationalization frameworks
- Languages other than English and Swedish in the initial release
- Automatic language detection based on IP address or geolocation
- Content localization for non-user-facing items (emails, reports, etc.)
- Right-to-left (RTL) language support
- Language-based feature flags or conditional functionality
- Automatic translation of user-generated content
- Ability to modify or negotiate terms of service
- Version history or diff views of legal documents
- Electronic signature capture beyond checkbox acceptance
- Language options beyond English and Swedish for legal documents
- Print-friendly or downloadable versions of the documents
- Multilingual support for the legal documents themselves
- A/B testing or variation of legal document presentation
- Caching of legal documents for extended periods (must check for updates)
- Data residency options beyond those explicitly supported by the system
- Automatic residency changes based on detected location changes
- Requiring residency selection to complete initial account creation; residency confirmation occurs during onboarding
- Ability to change residency after initial onboarding completion
- Residency-based feature flags or conditional functionality
- Data partitioning or sharding based on residency
- Legal advice or interpretation of residency regulations
- Integration with external residency verification services
- Residency confirmation via government ID or documentation

## Traceability

- Included Use Case IDs: UC-CCEF-005, UC-CCEF-007, UC-CCEF-008
- Architectural Assumptions:
  - The system follows a modular monolith architecture with clear boundaries (ADR-0001)
  - Language translations are managed via a standard i18n framework with message catalogs
  - The system stores user language preference as a locale string (e.g., 'en', 'sv')
  - Legal documents are stored as versioned HTML or markdown files
  - The system implements a consent management system that records versioned consent for legal documents
  - Data residency is determined via IP-to-location lookup service with configurable allowed regions
  - The system stores residency region as a string (e.g., 'EU', 'DE', 'FR')
  - The system uses AES-256-GCM to encrypt audit log entries containing PII (residency, consent)
  - HTTP 1.2 or higher is used for all external service calls (IP lookup, etc.)
  - The system implements caching for IP lookup service to improve performance
  - Residency region cannot be changed after onboarding to ensure data storage compliance
- Required ADRs: ADR-0001, ADR-0002
- Quality Gates:
  - Language detection must respect user's browser/OS language settings
  - Language selection must be offered as a clear choice between English and Swedish
  - All user-facing text must accurately translate to the selected language
  - Legal documents must be presented in the user's selected language
  - Acceptance checkboxes for legal documents must not be pre-checked
  - User must not be able to proceed without accepting both legal documents
  - Data residency inference must default to Europe as minimum supported region
  - System must prevent selection of unsupported residency regions
  - Selected or inferred residency must be recorded with timestamp and user ID
  - Residency region must be viewable but not changeable in account settings after onboarding
- Demo Criteria:
  - Demonstrate language detection and pre-selection based on browser/OS
  - Show user manually selecting English or Swedish language
  - Show interface updating to selected language in real-time
  - Demonstrate language persistence across sessions
  - Show terms & conditions and privacy policy presentation during onboarding
  - Demonstrate explicit acceptance of legal documents (scroll to bottom, unchecked checkbox)
  - Show system preventing progression without legal acceptance
  - Demonstrate data residency inference from IP address
  - Show user selecting alternative residency region where permitted
  - Show system recording and displaying residency region
  - Demonstrate residency region view in account settings (read-only)
- Acceptance Criteria:
  - System detects user's browser or operating system language
  - System pre-selects the detected language if it's English or Swedish, otherwise defaults to English
  - User can manually select English or Swedish from the language options
  - User's selection is saved to their account profile
  - Interface immediately updates to reflect the selected language
  - Language preference persists across sessions and page reloads
  - User can change their language preference at any time in account settings
  - System provides language names in both English and Swedish for selection clarity
  - All user-facing text in the interface translates to the selected language
  - During onboarding, users are presented with and must accept the terms & conditions and privacy policy before completing account creation
  - System presents clear, readable versions of both terms & conditions and privacy policy
  - Documents are presented in the user's selected language (English or Swedish)
  - User must scroll to the bottom of each document to enable the acceptance checkbox
  - Acceptance checkboxes are not pre-checked, requiring explicit user action
  - System records acceptance of both documents with timestamp and user ID
  - User cannot proceed with account creation without accepting both documents
  - System provides links to view the full documents in a modal or new page
  - Acceptance is stored durably and can be retrieved for audit purposes
  - System indicates which specific version of each document was accepted
  - During onboarding, the system infers the user's data residency region from IP address, with Europe as the minimum supported region
  - When inference is confident and region is supported, system pre-selects that region
  - When inference fails or region is unsupported, system prompts user to select region
  - Europe is presented as the minimum supported residency region
  - Users can select another supported region where regulation permits choice
  - System clearly indicates when residency is inferred vs. user-selected
  - System prevents selection of unsupported regions with clear explanation
  - System does not silently assign users to arbitrary regions when residency cannot be determined
  - Selected or inferred residency is recorded with timestamp and user ID
  - System provides explanation of what data residency means for the user
  - User can view their recorded residency in account settings (but not change it after onboarding)
  - System handles edge cases like VPNs, proxies, and mobile roaming appropriately

## Release Branches

1. Release branch creation happens only after Human green-light.

## Artifacts

- Completion Evidence: None.

### Coverage Matrix

| Requirement ID | Covered In This Milestone? | Fully/Partially Covered | Validation Method |
|---|---|---|---|
| FR-CCEF-001 | True | Complete | Covered in Milestone 1; verified to still work |
| FR-CCEF-002 | True | Complete | Covered in Milestone 1; verified to still work |
| FR-CCEF-003 | True | Complete | Covered in Milestone 1; verified to still work |
| FR-CCEF-004 | True | Complete | Covered in Milestone 1; verified to still work |
| FR-CCEF-005 | True | Complete | Covered in Milestone 1; verified to still work |
| FR-CCEF-006 | True | Complete | Covered in Milestone 1; verified to still work |
| FR-CCEF-007 | True | Complete | Covered in Milestone 1; verified to still work |
| FR-CCEF-009 | True | Complete | Covered in Milestone 1; verified to still work |
| FR-CCEF-015 | True | Complete | Covered in Milestone 1; verified to still work |
| FR-CCEF-018 | True | Complete | Covered in Milestone 2; verified to still work |
| FR-CCEF-019 | True | Complete | Covered in Milestone 2; verified to still work |
| FR-CCEF-020 | True | Complete | Covered in Milestone 2; verified to still work |
| FR-CCEF-021 | True | Complete | Covered in Milestone 2; verified to still work |
| FR-CCEF-022 | True | Complete | Unit tests for language detection logic; integration tests verifying language selection flow |
| FR-CCEF-023 | True | Complete | Unit tests for language persistence logic; integration tests verifying language change in settings |
| FR-CCEF-024 | False | Not Covered | N/A |
| FR-CCEF-025 | False | Not Covered | N/A |
| FR-CCEF-026 | False | Not Covered | N/A |
| FR-CCEF-027 | False | Not Covered | N/A |
| FR-CCEF-028 | False | Not Covered | N/A |
| FR-CCEF-029 | False | Not Covered | N/A |
| FR-CCEF-030 | False | Not Covered | N/A |
| FR-CCEF-031 | True | Complete | Unit tests for legal document presentation logic; integration tests verifying acceptance flow |
| FR-CCEF-032 | True | Complete | Unit tests for IP-based residency inference; integration tests verifying residency selection flow |
| NFR-CCEF-001 | True | Complete | Covered in Milestone 1; verified to still work |
| NFR-CCEF-002 | True | Complete | Covered in Milestone 1; verified to still work (benchmarks still met) |
| NFR-CCEF-003 | True | Complete | Covered in Milestone 2; verified to still work |
| NFR-CCEF-004 | True | Complete | Covered in Milestone 1; verified to still work |
| NFR-CCEF-005 | True | Complete | Covered in Milestone 1; verified to still work |
| NFR-CCEF-006 | True | Complete | Covered in Milestone 1; verified to still work |
| NFR-CCEF-007 | True | Complete | Covered in Milestone 1; verified to still work |
| NFR-CCEF-008 | True | Complete | Unit tests for language preference storage; integration tests verifying language change in settings |
| NFR-CCEF-009 | True | Complete | Unit tests for legal consent record integrity; integration tests verifying tamper-evidence |

### Increment Integrity

- Can this milestone be demoed independently? Yes.
- Can this milestone be deployed safely? Yes.
- What feature flags or disabled paths are required? Account settings UI is hidden; SMS consent feature can be toggled off; language selection limited to English/Swedish; legal acceptance and data residency steps can be skipped via feature flag
- What user-visible behavior is intentionally incomplete? Account settings interface is not accessible; SMS alerts are not sent (only consent is captured from Milestone 2); language preference cannot be changed after initial selection (no settings access); legal acceptance and data residency steps are not presented if feature flags are off
