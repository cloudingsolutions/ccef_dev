Requirement ID: NFR-CCEF-009
Title: Classification-based data encryption at rest
Requirement Type: non_functional
Product Slice IDs: PS-CCEF-001
Lifecycle State: Approved

# Requirement Statement
The system shall apply encryption at rest to persistent storage that contains user data based on data classification: baseline storage-layer encryption for persistent stores, and stronger application/envelope encryption for sensitive user data categories (credentials, tokens, secrets, provider access config, and PII as defined by data policy).

# Rationale
Encryption at rest is a fundamental security control that protects user data from unauthorized access. Applying baseline encryption via managed storage/services ensures protection against physical theft and unauthorized system access. Sensitive data categories receive additional application-layer envelope encryption to mitigate risks from privileged access or storage-layer breaches. This tiered approach aligns with data minimization and proportionality principles, meeting compliance requirements while avoiding unnecessary performance overhead.

# Acceptance Criteria
- Given the system stores user data persistently
- When user data is written to storage
- Then the system shall ensure baseline encryption at rest is applied via storage-layer encryption (e.g., transparent data encryption, cloud provider storage encryption) for persistent storage containing user data, including databases, file systems, backups, and caches where applicable
- And for sensitive user data categories (credentials, tokens, secrets, provider access config, PII), the system shall apply application/envelope encryption using AES-256-GCM or equivalent authenticated encryption algorithm before persistence
- And encryption keys for application-layer encryption shall be managed via a secure key management service (KMS) or hardware security module (HSM)
- And the system shall perform regular key rotation for application-layer encryption keys according to security best practices (minimum every 90 days)
- And encrypted data shall be decryptable only by authorized system components with proper access controls
- And the system shall maintain logs of encryption key access and usage for audit purposes
- And the system shall document the data classification policy that defines sensitive user data categories

# Explicit Exclusions
- Encryption of data in transit (covered by TLS requirements)
- Encryption of non-user data such as system logs or temporary cache (unless containing user data)
- Client-side encryption (encryption performed before data reaches the system)
- Application-layer or field-level encryption for non-sensitive user-associated data, which may rely on approved storage-layer encryption and access controls

# Constraints
- The system shall use AES-256-GCM or equivalent authenticated encryption algorithm for application-layer encryption of sensitive data
- Baseline storage-layer encryption shall be enabled for persistent stores handling user data
- Encryption key management for application-layer encryption shall follow industry best practices (NIST SP 800-57 or equivalent)
- The initial release must meet GDPR as the minimum compliance baseline for data protection
- Application-layer encryption shall not significantly impact system performance (target: <5% latency increase for storage operations)
- Key rotation for application-layer encryption keys shall be automated and transparent to users where possible
- Data classification policy shall be defined and approved prior to implementation

# Validation Method
- security review
- penetration testing
- configuration/infrastructure verification (verify baseline storage-layer encryption is enabled)
- automated test (verify application-layer encryption/decryption functionality)
- code review (verify encryption implementation and key management)
- compliance review (verify alignment with data classification policy and GDPR)

# References
- Related Requirements, non-blocking:
- ADRs: ADR-CCEF-002
- API / Data Contracts:
- Policies / Regulations: GDPR Article 32 (security of processing), NIST SP 800-57, ISO/IEC 27001
- Design Artifacts: Data Classification Policy (to be defined)
- Other:

# Traceability
- Product Slices: PS-CCEF-001
- Use Cases: (Cross-cutting requirement - supports all use cases)
