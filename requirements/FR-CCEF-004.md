Requirement ID: FR-CCEF-004
Title: Cloud provider access and discovery
Requirement Type: functional
Product Slice IDs: PS-CCEF-001
Lifecycle State: Approved

# Requirement Statement
The system shall allow users to securely provide read-only cloud provider access information for AWS, Google Cloud, and Azure, securely store and use the required provider credentials or access configuration, and retrieve supported services, inventory, usage/cost, and useful historical usage where available while distinguishing partial/unavailable data from discovered facts.

# Rationale
This requirement enables the core functionality of connecting to cloud providers to gather cost and usage data for forecasting, ensuring secure handling of credentials and proper interpretation of discovered data.

# Acceptance Criteria
- Given a user wants to connect cloud provider accounts for forecasting
- When the user provides read-only cloud provider access information for AWS, Google Cloud, or Azure using OAuth 2.0 or API keys
- Then the system shall securely store the required provider credentials using AES-256 encryption at rest and use them only for read-only API calls
- And the system shall retrieve supported services, inventory, usage/cost, and useful historical usage where available
- And the system shall distinguish partial/unavailable data from discovered facts by marking incomplete data with a `dataCompleteness: "partial"` flag in API responses
- Given historical usage is available from connected providers
- When generating forecasts
- Then the system may use historical usage to improve forecasts with a maximum lookback of 24 months
- Given the user does not provide growth expectations
- When generating forecasts
- Then the system shall use versioned benchmark growth assumptions (updated quarterly)
- Given user-provided growth assumptions are available
- When generating forecasts
- Then user-provided growth assumptions shall take priority over system defaults
- Given the cloud provider API is temporarily unavailable or returns an error
- When attempting to discover or retrieve data
- Then the system shall return HTTP 503 Service Unavailable with retry-after header and store the error in user-facing dashboard with clear messaging
- Given invalid or insufficient permissions are provided for cloud provider access
- When attempting to validate credentials
- Then the system shall return HTTP 403 Forbidden with specific error message about insufficient permissions and guide user to correct settings

# Explicit Exclusions
- Write access to cloud provider resources
- Automatic modification of cloud resources based on recommendations
- Access to unsupported cloud providers
- Collection of usage data without explicit user consent for provider access

# Constraints
- Users can securely provide read-only cloud provider access information for AWS, Google Cloud, and Azure using OAuth 2.0 (Authorization Code flow) or API keys with least privilege principle
- The system securely stores and uses the required provider credentials or access configuration using AES-256-GCM encryption at rest and TLS 1.2+ for data in transit
- Discovery retrieves supported services, inventory, usage/cost, and useful historical usage where available, while distinguishing partial/unavailable data from discovered facts with explicit data completeness flags
- The dataCompleteness flag shall have exactly three allowed values: "complete" (all expected data available), "partial" (some expected data missing/unavailable), and "unavailable" (no expected data available)
- Where historical usage is available, the system may use it to improve forecasts with a maximum lookback of 24 months
- User-provided growth assumptions take priority over system defaults
- Forecast formulas, supported units, currency rules (supported currencies: USD, EUR, SEK), rounding, horizons, and benchmark versions are deterministic enough for test oracles (±0.01% tolerance)
- Provider data discovery shall complete within 30 seconds for accounts with <1000 resources or return partial data with timeout notification
- The system shall implement exponential backoff retry mechanism (max 3 attempts) for provider API calls

# Validation Method
- automated test
- manual QA
- code review
- security review

# References
- Related Requirements, non-blocking:
- ADRs:
- API / Data Contracts: Cloud provider APIs (AWS, GCP, Azure)
- Policies / Regulations:
- Design Artifacts:
- Other:

# Traceability
- Product Slices: PS-CCEF-001
- Use Cases: UC-CCEF-004, UC-CCEF-005
