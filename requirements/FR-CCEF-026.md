# Requirement

- Requirement ID: FR-CCEF-026
- Title: User can update default language preference
- Requirement Type: functional
- Product Slice IDs: PS-CCEF-001
- Lifecycle State: Approved

## Requirement Statement
The system shall allow authenticated users to update their default language preference between English and Swedish, with immediate application of the selected language to the interface.

## Rationale
Users need to be able to interact with the system in their preferred language, and this preference should persist across sessions and be immediately applied.

## Acceptance Criteria
- Given the user is authenticated and viewing their account settings
- When the user selects a different language preference (English or Swedish) and saves the change
- Then the system shall save the new language preference to the user's account
- And the system shall immediately update the user interface to reflect the selected language
- And the system shall display a confirmation message that the language has been updated
- Given the user's current language is English
- When the user selects Swedish and saves the change
- Then all interface text, labels, and messages shall be displayed in Swedish
- Given the user's current language is Swedish
- When the user selects English and saves the change
- Then all interface text, labels, and messages shall be displayed in English

## Explicit Exclusions
This requirement does not include:
- Supporting languages beyond English and Swedish
- Automatic language detection based on browser settings
- Right-to-left language support
- Dialect or regional variations of English or Swedish
- Translation of user-generated content

## Constraints
- Only two language options are supported: English (en) and Swedish (sv)
- Language preference must be stored as a standardized locale code (en, sv)
- System must use proper internationalization (i18n) framework for language switching
- Language change must persist across user sessions
- Language change must be applied immediately without requiring page refresh (where technically feasible)
- System must fall back to English if translation files are missing for a particular language
- Language preference change must be logged in the audit trail

## Validation Method
- automated test
- manual QA
- code review

## References
- Related Requirements, non-blocking: FR-CCEF-024, FR-CCEF-025, FR-CCEF-027
- ADRs:
- API / Data Contracts: PATCH /api/v1/account/preferences endpoint
- Policies / Regulations:
- Design Artifacts: Account settings UI mockups
- Other: Language translation files (.json or .yaml format)

## Traceability
- Product Slices: PS-CCEF-001
- Use Cases: UC-CCEF-006