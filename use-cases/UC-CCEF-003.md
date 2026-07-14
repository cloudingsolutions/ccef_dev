# Use Case

- Use Case ID: UC-CCEF-003
- Title: User creates a manual cloud cost forecast
- Product Slice ID: PS-CCEF-001
- Lifecycle State: Approved

## Summary
A registered user manually defines provider services, usage assumptions, pricing adjustments, growth expectations, budget inputs, and forecast horizon to generate a deterministic future cloud cost forecast.

## Actor
Registered user

## Trigger
The user wants to estimate future cloud infrastructure costs without connecting a cloud provider account.

## Outcome
The system generates a manual cost forecast for the selected AWS, Google Cloud, or Azure services and displays forecasted costs, assumptions, benchmark basis where used, and any input correction guidance in the responsive web interface.

## Success Criteria
- The user can select or enter cloud services for AWS, Google Cloud, or Azure.
- The user can provide current or expected usage levels using supported units.
- The user can define or tune growth expectations.
- The user can adjust pricing assumptions and selected forecast currency within supported rules.
- The user can choose a supported forecast horizon.
- The system generates and displays a forecast from manually entered data using deterministic calculation, rounding, and benchmark rules.
- Manual forecast creation, saved forecast access, forecast display, budget inputs, assumptions, and forecast outputs are available only within a valid registered-user session and are limited to forecast objects owned by or otherwise authorized for that authenticated user.
- Invalid numeric inputs are blocked with field-level recovery guidance while preserving valid user input.
- Forecast setup, errors, assumptions, benchmark explanations, and results support English and Swedish for the initial release.
- The user can save a manually created forecast to their forecast library with a name and description.
- The user can edit a saved forecast and choose to save changes as a new version or overwrite the existing forecast.
- The user can duplicate a saved forecast.
- The user can delete a saved forecast after explicit confirmation.
- The user can compare two or more saved forecasts (up to 5) in a side-by-side view.
- The user can view the version history of a saved forecast.
- All forecast management actions provide localized (English/Swedish) confirmation dialogs, status messages, and recovery guidance.

## Explicit Exclusions
- Invoice reconciliation
- Billing system replacement
- Automated cloud resource changes
- Hidden currency conversion for manual inputs

## Linked Requirement IDs
- FR-CCEF-005
- FR-CCEF-006
- FR-CCEF-010  (User dashboard and home experience)
- FR-CCEF-012  (Forecast management capabilities)
- NFR-CCEF-013  (Observability and monitoring requirements)