# Architectural Decision Record

- ADR ID: ADR-CCEF-002
- Title: Data Encryption and Key Management Strategy
- Status: Approved
- Product Slice IDs: PS-CCEF-001
- Related Requirement IDs: NFR-CCEF-009, PRI-CCEF-001, PRI-CCEF-003, PRIV-CCEF-001
- Related Milestone IDs:
- Decision: Apply baseline storage-layer encryption (e.g., transparent data encryption, cloud provider storage encryption) to persistent storage handling user data. For sensitive user data categories (credentials, tokens, secrets, provider access config, PII), apply application/envelope encryption using AES-256-GCM authenticated encryption with keys managed via a cloud-native Key Management Service (KMS) (e.g., AWS KMS, Google Cloud KMS, Azure Key Vault) with automatic key rotation every 90 days. Non-sensitive user-associated records may rely on approved storage-layer encryption and access controls; this decision does not require field-level encryption for every user-associated field. Maintain audit logs of key access and usage for application-layer encryption.
- Context: The system must protect user data confidentiality and comply with GDPR and other privacy regulations. Requirements mandate encryption at rest for user data, with a tiered approach based on data classification: baseline encryption for persistent stores that contain user data via storage-layer controls, and stronger application-layer encryption for sensitive categories. This balances security, performance, and operational complexity.
- Options Considered:
  1. Uniform application-level encryption for all user-associated records using a library (e.g., libsodium) with self-managed keys.
  2. Uniform transparent data encryption (TDE) offered by the database/provider storage for persistent stores that contain user data.
  3. Hybrid approach: baseline storage-layer encryption for persistent stores that contain user data, plus application-level envelope encryption for sensitive data using cloud KMS (chosen).
  4. Application-level encryption with cloud KMS for all user-associated records (previous approach).
- Consequences:
  - Pros: Strong protection for sensitive data via envelope encryption; baseline encryption provides defense-in-depth for persistent stores that contain user data; reduced performance impact as only sensitive data incurs application-layer overhead; key rotation automation for application-layer keys; auditability; compliance with GDPR and data minimization principles.
  - Cons: Slight latency increase for sensitive data operations (<5% target); dependency on KMS availability for application-layer encryption; need to manage key access policies and data classification implementation; increased complexity in encryption strategy.
- Constraints Imposed:
  - Use AES-256-GCM or equivalent authenticated encryption algorithm for application-layer encryption of sensitive data.
  - Baseline storage-layer encryption shall be enabled for persistent stores handling user data (e.g., database TDE, storage service encryption).
  - Encryption key management for application-layer encryption follows NIST SP 800-57 or equivalent.
  - Automated key rotation minimum every 90 days for application-layer encryption keys.
  - Encrypted data (application-layer) decryptable only by authorized system components.
  - Maintain logs of application-layer encryption key access and usage for audit.
  - Application-layer encryption shall not significantly impact system performance (<5% latency increase for storage operations).
  - Data classification policy shall be defined and approved, identifying sensitive user data categories.
- Files / Modules Affected:
  - src/backend/security/encryption/ (encryption service for application-layer)
  - src/backend/config/kms/ (KMS client configuration for application-layer keys)
  - src/backend/models/ (encryption fields in data models for sensitive data)
  - src/backend/audit/ (key access logging for application-layer keys)
  - src/backend/services/ (services that store/retrieve data; will invoke encryption service for sensitive data)
  - src/backend/storage/ (configuration to ensure baseline storage-layer encryption is enabled)
- Validation Method:
  - Security review of encryption implementation and key management for both baseline and application-layer.
  - Penetration testing to verify resistance to data leakage and that sensitive data is protected with envelope encryption.
  - Automated tests for encryption/decryption functionality for application-layer encryption.
  - Code review to ensure encryption is applied per data classification (baseline via storage config, application-layer via service calls).
  - Compliance verification against GDPR Article 32 and NIST SP 800-57.
  - Verification that baseline storage-layer encryption is enabled (e.g., via infrastructure as code review).
