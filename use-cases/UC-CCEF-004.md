# Use Case

- Use Case ID: UC-CCEF-004
- Title: User connects a cloud provider account for discovery
- Product Slice ID: PS-CCEF-001
- Lifecycle State: Approved

## Summary
A registered user securely provides supported read-only access configuration for AWS, Google Cloud, or Azure so the system can discover current services, inventory, usage, cost, and useful historical usage where available.

## Actor
Registered user

## Trigger
The user wants the system to forecast costs using provider-discovered cloud data instead of only manual entries.

## Outcome
The cloud provider connection is stored and usable for retrieving provider usage and inventory data within the slice scope using the minimum access needed for discovery-oriented retrieval, or the user receives safe recovery guidance when setup fails or is incomplete.

## Success Criteria
- The user can securely provide cloud provider access information for AWS, Google Cloud, or Azure.
- The system securely stores and uses the required provider credentials or access configuration.
- The product requests or documents only the minimum provider permissions required for discovery, inventory, usage, cost, and useful historical usage retrieval, and does not require write or remediation privileges.
- Provider connection failures explain safe recovery options without exposing secrets.
- For connected providers, the system can retrieve services currently in use.
- For connected providers, the system can retrieve relevant inventory and usage/cost data.
- Where available and useful for forecasting, the system can retrieve historical usage data.
- Partial discovery distinguishes available and unavailable categories without fabricating provider data.

## Explicit Exclusions
- Automated remediation of cost issues
- Automated cloud resource changes
- Advanced FinOps approval workflows

## Linked Requirement IDs
- FR-CCEF-004
- FR-CCEF-005
- FR-CCEF-010  (User dashboard and home experience)
- FR-CCEF-011  (Provider connection management)
- FR-CCEF-012  (Forecast management capabilities)
- NFR-CCEF-013  (Observability and monitoring requirements)