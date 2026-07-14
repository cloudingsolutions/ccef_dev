# Use Case

- Use Case ID: UC-CCEF-005
- Title: User generates a forecast from discovered provider usage
- Product Slice ID: PS-CCEF-001
- Lifecycle State: Approved

## Summary
A registered user generates a future cost forecast using discovered services, inventory, current usage/cost, and historical usage from a connected AWS, Google Cloud, or Azure account.

## Actor
Registered user

## Trigger
The user has connected a supported provider account and wants a forecast based on actual discovered cloud usage.

## Outcome
The system generates and displays a provider-based cost forecast using discovered usage and forecast assumptions, while clearly labeling partial or unavailable provider data and avoiding fabricated values.

## Success Criteria
- The system uses discovered provider services and usage/cost data to generate the forecast.
- The system may use historical usage to improve forecasts where available and useful.
- The user can override or tune pricing and growth assumptions before or after forecast generation.
- User-provided growth assumptions take priority over system defaults.
- If the user does not provide growth expectations, the system uses the active versioned benchmark growth assumptions.
- The user can choose a supported forecast horizon.
- Partial provider discovery is visible in the forecast basis and missing data is not fabricated.
- Forecast results, assumptions, benchmark context, partial-data states, and recovery guidance support English and Swedish for the initial release.
- The user can save a generated forecast to their forecast library with a name and description.
- The user can edit a saved forecast and choose to save changes as a new version or overwrite the existing forecast.
- The user can duplicate a saved forecast.
- The user can delete a saved forecast after explicit confirmation.
- The user can compare two or more saved forecasts (up to 5) in a side-by-side view.
- The user can view the version history of a saved forecast.
- All forecast management actions provide localized (English/Swedish) confirmation dialogs, status messages, and recovery guidance.

## Explicit Exclusions
- Reserved instance, savings plan, committed use, or contract purchasing guidance
- Invoice reconciliation
- Automated cloud resource changes

## Linked Requirement IDs
- FR-CCEF-004
- FR-CCEF-005
- FR-CCEF-006
- FR-CCEF-010  (User dashboard and home experience)
- FR-CCEF-011  (Provider connection management)
- FR-CCEF-012  (Forecast management capabilities)
- NFR-CCEF-013  (Observability and monitoring requirements)