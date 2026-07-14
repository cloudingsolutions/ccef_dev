# Data Handling Policy

This document defines the category-specific retention, export, deletion, and provider-disconnect behavior for the Cloud Cost Estimator and Forecaster system. It also defines confirmation requirements, localized status/recovery states, audit evidence generation, and stale data handling for privacy-related actions.

## Operational Behavior Requirements

### Confirmation Behavior
- All privacy-related actions (export, deletion, provider disconnect) shall require explicit user confirmation.
- Confirmation dialogs shall clearly identify:
  - The specific action being performed (export, deletion, or provider disconnect)
  - The data categories affected by the action
  - The consequences of the action, including what data will be exported, deleted, retained, and what will happen to provider connections
  - Any irreversible consequences of the action
- Confirmation shall require explicit affirmative action, such as selecting a confirmation control.
- Users shall be able to cancel the action at the confirmation step.

### Localized Status and Recovery States
- During execution of privacy-related actions, the system shall display localized status messages.
- Status messages shall indicate progress where applicable, such as preparing export, deleting data, or disconnecting provider.
- Upon completion, the system shall display localized success or recovery messages.
- Success messages shall confirm what was accomplished.
- Recovery messages shall provide next-step guidance when useful, such as reconnecting a provider or downloading exported data.
- All status and recovery messages shall be localized to the user's selected language, English or Swedish.

### Audit Evidence Generation
- The system shall generate audit evidence for all privacy-related actions.
- Audit evidence shall include:
  - Timestamp of the action in ISO 8601 format
  - User ID initiating the action
  - Action type: `EXPORT`, `DELETE`, or `PROVIDER_DISCONNECT`
  - Data categories affected
  - Outcome: `SUCCESS`, `FAILURE`, or `CANCELLED`
  - For export actions: file format, size, and download link or reference
  - For deletion actions: confirmation of deletion initiation and expected completion timeframe
  - For provider disconnect actions: provider identifier and disconnection timestamp
- Audit evidence shall be stored in an immutable, write-once format suitable for compliance purposes.
- Audit evidence shall be accessible for security and compliance reviews.

### Stale Data Handling
- When provider-derived data becomes stale due to provider disconnect or data deletion requests, the system shall handle it according to defined rules.
- Stale data shall be marked as inaccessible for normal operations.
- The system shall provide clear indicators when data is stale, such as visual indicators, labels, or messages.
- Stale data shall be retained for a defined grace period before permanent deletion to allow recovery when applicable.
- During the grace period, stale data shall not be used for forecasting, budgeting, alert generation, or other operational purposes.
- After the grace period, stale data shall be permanently deleted according to secure deletion practices.
- The system shall provide users with visibility into stale data status and expected deletion timelines.

## Data Categories and Handling

### Account Data
- **Retention**: Retained until deletion
- **Export Format**: JSON or XML
- **Deletion**: Deleted immediately upon request
- **Provider Disconnect**: Marks as orphaned (retains data but flags as disconnected)

### Phone Data
- **Retention**: Retained 90 days post-deletion for fraud prevention
- **Export Format**: CSV
- **Deletion**: Deleted after retention period
- **Provider Disconnect**: No effect (retains data for 90 days post-deletion regardless)

### Consent Data
- **Retention**: Retained 7 years for compliance audit
- **Export Format**: JSON
- **Deletion**: Deleted after retention period
- **Provider Disconnect**: Preserves consent records

### Provider Credential/Configuration Data
- **Retention**: Encrypted until deletion
- **Export Format**: Masked format (last 4 characters only)
- **Deletion**: Deleted immediately upon provider disconnect
- **Post-Deletion**: Zero-retention after deletion

### Provider Inventory/Usage/History Data
- **Retention**: Retained 24 months for forecasting
- **Export Format**: CSV
- **Deletion**: 
  - Deleted after retention period
  - OR immediately upon provider disconnect with user confirmation
- **Provider Disconnect**: Can trigger immediate deletion with user confirmation

### Forecast Data
- **Retention**: Retained 12 months
- **Export Format**: JSON
- **Deletion**: Deleted after retention period
- **Provider Disconnect**: No effect on manual forecasts

### Budget Data
- **Retention**: Retained 24 months
- **Export Format**: JSON
- **Deletion**: Deleted after retention period
- **Provider Disconnect**: Preserves budget configurations

### Alert/Anomaly Data
- **Retention**: Retained 12 months
- **Export Format**: JSON
- **Deletion**: Deleted after retention period
- **Provider Disconnect**: Preserves alert configurations

### SMS Delivery Metadata
- **Retention**: Retained 6 months for billing disputes
- **Export Format**: CSV
- **Deletion**: Deleted after retention period
- **Provider Disconnect**: No effect

### Audit Log
- **Retention**: Retained 7 years for compliance
- **Export Format**: JSON or XML
- **Storage**: Write-once storage (immutable)
- **Provider Disconnect**: No effect

### Derived Data
- **Retention**: Retained according to source data retention
- **Export Format**: Exported in same format as source
- **Deletion**: Follows source data deletion rules
- **Provider Disconnect**: Follows source data provider-disconnect behavior

## Data Handling Principles

1. **Transparency**: All data handling practices are documented and available to users
2. **Purpose Limitation**: Data is only retained for the specified purposes
3. **Data Minimization**: Only necessary data is collected and retained
4. **Storage Limitation**: Data is not retained longer than necessary
5. **Integrity and Confidentiality**: Appropriate security measures protect data
6. **Accountability**: The system logs all data handling actions for audit purposes

## Compliance

This policy is designed to meet GDPR as the minimum compliance baseline, with provisions to support additional privacy regimes including LGPD, CPRA/CCPA-family obligations, and other regional privacy requirements as market expansion requires.

Relevant GDPR articles include Articles 5 (principles), 15 (access), 16 (rectification), 17 (erasure), 20 (portability), and 30 (records of processing activities).

## Review and Updates

This policy shall be reviewed:
- Before each implementation cycle
- Annually at minimum
- When significant changes to data handling practices are proposed
- When new privacy regulations take effect that impact the service

## Related Requirements

- PRI-CCEF-009: Data retention, export, deletion, and provider-disconnect behavior
- PRI-CCEF-003: Privacy controls for account/data export, deletion, and provider disconnect
- NFR-CCEF-008: Localization and accessibility compliance
- NFR-CCEF-013: Observability and monitoring requirements
