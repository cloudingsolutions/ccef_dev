# Use Case

- Use Case ID: UC-CCEF-002
- Title: User signs in and manages their basic account
- Product Slice ID: PS-CCEF-001
- Lifecycle State: Approved

## Summary
A registered user signs in to the responsive web application and manages the basic account settings needed to use forecasting and alert features, including default language and basic notification/contact preferences.

## Actor
Registered user

## Trigger
The user needs to access or update their account before forecasting or alert configuration.

## Outcome
The user reaches the authenticated product experience and can manage basic account settings needed by the slice, including changing default language after onboarding and maintaining basic contact or notification preferences for production alert setup.

## Success Criteria
- The registered user can sign in successfully.
- The user can manage basic account information needed for cloud cost forecasting and alert setup.
- The account experience supports the user's selected default language.
- The user can change their default language after onboarding, with English and Swedish supported in the initial release.
- The user can manage basic notification or contact preferences needed for in-app/dashboard and SMS alert setup within the initial production scope.
- The account experience remains within basic registered-user access scope.

## Explicit Exclusions
- Team role management
- Organization-level administration
- Complex approval or FinOps workflows
- Advanced notification workflow configuration beyond basic initial production account and alert preferences

## Linked Requirement IDs
- FR-CCEF-002
- FR-CCEF-010  (User dashboard and home experience)
- FR-CCEF-011  (Provider connection management)
- FR-CCEF-012  (Forecast management capabilities)
- NFR-CCEF-013  (Observability and monitoring requirements)