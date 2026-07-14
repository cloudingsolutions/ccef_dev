# Architectural Decision Record

- ADR ID: ADR-CCEF-010
- Title: Data Residency and Localization Strategy
- Status: Approved
- Product Slice IDs: PS-CCEF-001
- Related Requirement IDs: FR-CCEF-001, NFR-CCEF-008 (Localization and accessibility compliance), PRI-CCEF-001 (subprocessor disclosure)
- Related Milestone IDs:
- Decision: Determine user data residency during onboarding using IP address and/or phone number where available and appropriate. Store residency as part of user profile. Provision user-specific data (e.g., forecasts, budgets, alerts) in logical storage partitions tied to the residency region (e.g., separate database schemas or prefixes) to facilitate compliance with data localization laws. Support European Union (EU) as the minimum supported residency region for the initial release; allow user to select another supported residency region (e.g., US East, Canada) where applicable regulation permits choice. For localization, maintain all user-facing content in English and Swedish; detect user's selected language from profile or onboarding choice and serve localized strings via i18n backend endpoints and frontend i18n library. Return language preference in HTTP response headers (Content-Language) and/or JWT claims for frontend consumption.
- Context: The product must comply with data residency regulations (e.g., GDPR) by not assigning users to arbitrary regions and honoring user choice where permitted. Additionally, the product must support English and Swedish languages for all in-scope core user-facing copy and alert content.
- Options Considered:
  1. Determine residency solely from IP address (less reliable with VPNs/proxies).
  2. Use phone number country code as primary signal (may not reflect actual residency).
  3. Combine IP and phone number with a decision policy (chosen).
  4. Allow full user selection without any automatic detection (risk of non-compliance if user picks unsupported region).
- Consequences:
  - Pros: Uses available signals to make informed residency determination; provides clear unsupported/indeterminate state when confidence low; supports user choice where regulation permits.
  - Cons: Need to maintain and update geolocation database; must handle edge cases where signals conflict.
- Constraints Imposed:
  - Determine residency using available signals: IP address (geolocation to country) and/or phone number (country code).
  - Europe (EU) is the minimum supported residency region for the initial release.
  - Where applicable regulation permits user choice, allow selection from a list of supported residency regions (to be defined per jurisdiction).
  - If residency is unsupported or cannot be determined with sufficient confidence, present a clear unsupported/indeterminate residency outcome (HTTP 409 Conflict) with guidance.
  - Store residency in user profile and enforce that any newly created user data is associated with that residency.
  - All user-facing content localized to English and Swedish; no other languages in initial release unless separately defined.
  - Use ISO 639-1 language codes (en, sv) for localization.
  - Return Content-Language header in HTTP responses matching user's selected language.
  - Include language preference in JWT claims (or retrieve via user service) for frontend.
- Files / Modules Affected:
  - src/backend/onboarding/ (residency determination logic)
  - src/backend/models/user.ts (add residency field)
  - src/backend/services/user-service.ts (Desprésidency updates)
  - src/backend/middleware/localization.ts (set Content-Language, load translations)
  - src/backend/utils/geo.ts (IP to country lookup using e.g., MaxMind DB)
  - src/backend/config/residency-regions.ts (list of supported regions per jurisdiction)
  - src/frontend/i18n/ (translation files)
  - src/frontend/utils/i18n.ts (i18n initialization hook)
- Validation Method:
  - Automated tests for residency determination with various IP/phone combinations.
  - Manual QA confirms unsupported/indeterminate states and user choice flow.
  - Code review ensures residency enforcement in data creation paths.
  - Localization verification: all UI strings appear in correct language.
  - Compliance review confirms alignment with GDPR residency principles and user choice where applicable.