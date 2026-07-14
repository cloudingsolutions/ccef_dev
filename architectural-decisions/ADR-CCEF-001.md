# Architectural Decision Record

- ADR ID: ADR-CCEF-001
- Title: Cloud Provider Abstraction and Integration Strategy
- Status: Approved
- Product Slice IDs: PS-CCEF-001
- Related Requirement IDs: FR-CCEF-004
- Related Milestone IDs:
- Decision: Use a provider-agnostic abstraction layer with adapter implementations for each supported cloud provider (AWS, Google Cloud, Azure). Authentication via OAuth 2.0 Authorization Code flow or API keys. Store provider credentials encrypted at rest using AES-256-GCM. Retrieve services, inventory, usage/cost, and historical usage; mark data completeness with a flag having three allowed values: "complete", "partial", "unavailable".
- Context: The system must allow users to connect read-only access to AWS, Google Cloud, and Azure accounts to gather cost and usage data for forecasting. The integration must be secure, support multiple providers, and distinguish between complete and partial data.
- Options Considered:
  1. Direct use of vendor-specific SDKs without abstraction layer (tight coupling, duplicated code).
  2. Adopt a third-party multi-cloud library (e.g., Terraform, Crossplane) for resource discovery.
  3. Build custom abstraction with adapters (chosen).
- Consequences:
  - Pros: Loose coupling between core logic and provider-specific implementations; easier to add new providers; consistent error handling and data modeling; centralized credential storage and encryption.
  - Cons: Initial development effort to build adapters; need to maintain adapters as provider APIs evolve.
- Constraints Imposed:
  - Credentials must be encrypted at rest using AES-256-GCM (per NFR-CCEF-009 and FR-CCEF-004).
  - All provider API calls must use TLS 1.2+.
  - Support OAuth 2.0 Authorization Code flow or API keys with least privilege.
  - Data completeness flag must have exactly three allowed values: "complete", "partial", "unavailable".
  - Provider data discovery must complete within 30 seconds for accounts with <1000 resources or return partial data with timeout.
  - Implement exponential backoff retry (max 3 attempts) for provider API calls.
- Files / Modules Affected:
  - src/backend/cloud-providers/ (adapter implementations)
  - src/backend/services/forecasting/ (usage of provider data)
  - src/backend/auth/ (credential storage and encryption)
  - src/backend/models/provider-data.ts (shared data models)
- Validation Method:
  - Automated unit and integration tests for each adapter.
  - Security review of credential storage and encryption.
  - Code review for adherence to abstraction layer contracts.
  - Contract tests to ensure adapter implementations meet the provider interface.