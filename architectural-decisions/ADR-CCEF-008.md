# Architectural Decision Record

- ADR ID: ADR-CCEF-008
- Title: SMS Integration Architecture
- Status: Approved
- Product Slice IDs: PS-CCEF-001
- Related Requirement IDs: FR-CCEF-007, NFR-CCEF-009
- Related Milestone IDs:
- Decision: Implement an SMS notification abstraction layer with adapter implementations for chosen SMS provider(s) (e.g., Twilio, AWS SNS). Store API credentials encrypted at rest using AES-256-GCM. Provide a unified sendSms(to, message, options) interface. Support localization of message content (English/Swedish). Implement rate limiting and exponential backoff retry (max 3 attempts). Honor opt-out and consent flags; do not send SMS if user has disabled SMS alerts or withdrawn consent.
- Context: The system must send SMS alerts for budget-risk conditions and anomaly detection when eligible and user has consented. Need to securely handle credentials, comply with telecommunications regulations, and provide localized messages.
- Options Considered:
  1. Direct integration with a single SMS provider (tight coupling).
  2. Use a third-party messaging abstraction layer (e.g., Vonage API).
  3. Build provider-agnostic adapter layer (chosen).
- Consequences:
  - Pros: Ability to switch providers, consistent error handling, centralized credential management.
  - Cons: Need to maintain adapters; must stay updated with provider API changes.
- Constraints Imposed:
  - SMS provider credentials encrypted at rest using AES-256-GCM (per NFR-CCEF-009).
  - Use HTTPS/TLS 1.2+ for provider API calls.
  - Implement rate limiting to stay within provider limits and avoid abuse.
  - Exponential backoff retry (max 3 attempts) on transient failures.
  - Localize SMS content to user's selected language (English/Swedish).
  - Check user consent and opt-out status before sending; respect do-not-call lists.
  - Include clear instructions for opting out in each SMS (if required by regulation).
- Files / Modules Affected:
  - src/backend/sms/ (adapter implementations and service)
  - src/backend/models/sms.ts (SMS message model)
  - src/backend/services/alert-service.ts (triggering SMS alerts)
  - src/backend/auth/ (encrypted credential storage)
  - src/backend/middleware/rate-limit.ts (SMS-specific rate limiting)
- Validation Method:
  - Automated tests for SMS service with mock providers.
  - Security review of credential storage and transmission.
  - Code review for adherence to abstraction and consent checks.
  - Manual testing with a test SMS provider account (or sandbox).
  - Compliance review for telecommunications regulations (e.g., TCPA, GDPR if personal data).