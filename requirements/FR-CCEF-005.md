Requirement ID: FR-CCEF-005
Title: Cloud cost forecasting capabilities
Requirement Type: functional
Product Slice IDs: PS-CCEF-001
Lifecycle State: Approved

# Requirement Statement
The system shall support two forecast paths: manual forecasting where users enter cloud services, usage assumptions, pricing adjustments, growth expectations, budget inputs, and forecast horizon; and provider-based forecasting where users connect a supported cloud provider account and the system retrieves current services, inventory, usage/cost, and useful historical usage through read-only provider APIs. The system shall allow users to generate forecasts from both manual entry and discovered provider data, override or tune pricing and growth assumptions, and choose a supported forecast horizon.

# Rationale
This requirement defines the core forecasting functionality that allows users to estimate future cloud costs through manual input or by leveraging actual usage data from connected cloud providers.

# Acceptance Criteria
- Given a registered user has completed onboarding and reached a supported residency outcome
- When the user wants to create a cloud cost forecast
- Then the user shall be able to manually create a deterministic cloud cost forecast for AWS, Google Cloud, or Azure by entering cloud services, usage assumptions, pricing adjustments, growth expectations, budget inputs, and forecast horizon with all monetary values rounded to 2 decimal places
- And the user shall be able to connect an AWS, Google Cloud, or Azure account with read-only minimum necessary access using OAuth 2.0 or API keys
- And the system shall allow the system to retrieve supported usage, cost, inventory, and historical data from the connected provider with HTTP 200 OK responses or appropriate error codes
- And the user shall be able to generate a forecast from manually entered data with results rounded to 2 decimal places and returned within 5 seconds for forecasts <12 months horizon
- And the user shall be able to generate a forecast from discovered provider usage without fabricating missing provider data, marking any estimated values with `isEstimated: true` flag
- And the user shall be able to override or tune pricing and growth expectations with validation ensuring values are between -50% and +500% of baseline
- And the user shall be able to generate a forecast using versioned benchmark growth assumptions (v1.0, updated quarterly) when no user growth input is provided
- And the user shall be able to choose a supported forecast horizon (1, 3, 6, 12, or 24 months)
- And the user shall be able to view forecasted cloud costs in a responsive, accessible web interface with chart/table alternatives showing values rounded to 2 decimal places
- Given the system encounters an error retrieving provider data
- When generating a forecast
- Then the system shall return partial forecast with available data and clear indication of missing data sources

# Explicit Exclusions
- Advanced optimization recommendations such as reserved instance, savings plan, committed use, or contract purchasing guidance
- Automated cloud resource changes
- Automated remediation of cost issues
- Invoice reconciliation or billing system replacement
- Team or organization role management beyond basic registered-user access
- Complex FinOps workflows, approval flows, or chargeback/showback reporting

# Constraints
- Users can manually provide or tune pricing and growth expectations within realistic bounds (-50% to +500% of baseline)
- If the user does not provide growth expectations, the system uses versioned benchmark growth assumptions (v1.0, updated quarterly based on public cloud provider pricing trends)
- Where historical usage is available, the system may use it to improve forecasts with a maximum lookback of 24 months
- User-provided growth assumptions take priority over system defaults
- Forecast formulas shall round all monetary values to exactly 2 decimal places using standard rounding rules (half-up)
- Forecast formulas, supported units, currency rules (supported currencies: USD, EUR, SEK), horizons, and benchmark versions are deterministic enough for test oracles with output variance not exceeding ±0.01% given identical inputs
- Users can choose a supported forecast horizon (1, 3, 6, 12, or 24 months)
- The responsive web experience must target WCAG 2.2 AA and remain usable at mobile, tablet, small desktop, and desktop layouts
- Forecast generation shall complete within 5 seconds for manual forecasts and 30 seconds for provider-based forecasts <12 months horizon
- The system shall cache provider data for up to 1 hour to reduce API calls while ensuring data freshness
- For test oracle purposes, forecast calculations shall produce identical results given identical inputs, with monetary values rounded to 2 decimal places and percentage values rounded to 4 decimal places

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
- Use Cases: UC-CCEF-003, UC-CCEF-004, UC-CCEF-005, UC-CCEF-006
