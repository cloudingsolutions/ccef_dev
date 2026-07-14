# Architectural Decision Record

- ADR ID: ADR-CCEF-009
- Title: Privacy Controls Implementation (Export, Deletion, Provider Disconnect)
- Status: Approved
- Product Slice IDs: PS-CCEF-001
- Related Requirement IDs: PRI-CCEF-003, PRIV-CCEF-001, PRI-CCEF-001
- Related Milestone IDs:
- Decision: Implement a centralized privacy service that coordinates export, deletion, and provider disconnect actions. For each action: require explicit user confirmation, generate audit evidence (ISO 8601 timestamp, user ID, action type, outcome, affected data categories), provide localized status/recovery messages, and handle stale data according to category-specific retention/grace periods. Export data in the formats specified (JSON, CSV, XML) per data category. Store audit logs in an immutable, write-once format. Mark provider-derived data as inaccessible upon disconnect and schedule purging after grace period.
- Context: Users must be able to exercise privacy rights (export, deletion, provider disconnect) with clear compliance to GDPR and other regulations. The system must provide consistent behavior across data categories, including confirmation, auditability, and proper handling of stale data.
- Options Considered:
  1. Implement each privacy action as scattered code in respective services (risk of inconsistency).
  2. Use a third-party privacy management platform.
  3. Centralized privacy service with prescribed behavior (chosen).
- Consequences:
  - Pros: Consistent behavior guaranteed, easier to audit and update, single source of truth for privacy logic.
  - Cons: Service must be carefully designed to avoid becoming a bottleneck; need to manage data category-specific rules.
- Constraints Imposed:
  - All privacy-related actions require explicit user confirmation step.
  - Confirmation must identify action, affected data categories, and consequences.
  - Localized status/recovery states displayed during and after action execution.
  - Audit evidence includes timestamp (ISO 8601), user ID, action type (ENUM: EXPORT, DELETE, PROVIDER_DISCONNECT), outcome (ENUM: SUCCESS, FAILURE, CANCELLED), data categories affected, and category-specific details.
  - Audit logs stored in write-once format (e.g., append-only storage or WORM) suitable for compliance.
  - Stale data handling: mark as inaccessible, retain for defined grace period, then purge securely.
  - Grace periods per data category as defined in PRIV-CCEF-001 (e.g., 90 days for phone data, 24 months for provider usage history with user confirmation, etc.).
  - All user-facing copy localized to English/Swedish.
- Files / Modules Affected:
  - src/backend/privacy/ (privacy service, controllers)
  - src/backend/models/audit-log.ts (audit entry model)
  - src/backend/services/ (services invoked by privacy actions: user-service, provider-service, forecast-service, etc.)
  - src/backend/middleware/privacy-confirmation.ts (confirmation middleware)
  - src/backend/workers/ (background workers for delayed purging of stale data)
  - src/backend/config/privacy-retention.ts (retention/grace period configuration)
- Validation Method:
  - Automated tests for each privacy action covering confirmation, audit logging, and stale data handling.
  - Manual QA verifies localized messages and correct export formats.
  - Code review ensures adherence to PRIV-CCEF-001 behavior.
  - Compliance review validates GDPR alignment (Articles 15, 16, 17, 20).
  - Security review confirms audit log integrity and confidentiality.