Requirement ID: FR-CCEF-002
Title: User sign-in and basic account management
Requirement Type: functional
Product Slice IDs: PS-CCEF-001
Lifecycle State: Approved

# Requirement Statement
The system shall allow registered users to sign in to the responsive web application and manage basic account settings needed to use forecasting and alert features, including default language and basic notification/contact preferences.

# Rationale
This requirement ensures users can access the system after registration and configure their basic preferences for language and notifications, which are essential for personalized experience and alert delivery.

# Acceptance Criteria
- Given a registered user needs to access or update their account before forecasting or alert configuration
- When the user attempts to sign in with valid credentials
- Then the system shall allow the user to sign in successfully returning HTTP 200 OK with JWT token and user profile
- And the user shall be able to manage basic account information needed for cloud cost forecasting and alert setup including display name, email preferences, and language settings
- And the account experience shall support the user's selected default language returning content in the selected language (English or Swedish)
- And the user shall be able to change their default language after onboarding between English and Swedish with HTTP 200 OK response confirming language change
- And the user shall be able to manage basic notification or contact preferences needed for in-app/dashboard and SMS alert setup within the initial production scope including:
  * Toggle for in-app notifications (enabled/disabled)
  * Toggle for SMS alerts (enabled/disabled)
  * Phone number field for SMS delivery (when SMS alerts enabled)
  * Email notification frequency options (immediate, daily digest, weekly digest)
- And the account experience shall remain within basic registered-user access scope without access to administrative or team management functions

# Explicit Exclusions
- Team role management
- Organization-level administration
- Complex approval or FinOps workflows
- Advanced notification workflow configuration beyond basic initial production account and alert preferences

# Constraints
- The product must support localization and user-selectable default language
- The initial release must support English and Swedish for all in-scope core user-facing copy and alert content
- Users can choose and later update English or Swedish as their default language

# Validation Method
- automated test
- manual QA
- code review

# References
- Related Requirements, non-blocking:
- ADRs:
- API / Data Contracts:
- Policies / Regulations:
- Design Artifacts:
- Other:

# Traceability
- Product Slices: PS-CCEF-001
- Use Cases: UC-CCEF-001, UC-CCEF-002
