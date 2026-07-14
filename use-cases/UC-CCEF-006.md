# Use Case

- Use Case ID: UC-CCEF-006
- Title: User reviews forecast results and basic cost insights
- Product Slice ID: PS-CCEF-001
- Lifecycle State: Approved

## Summary
A registered user views forecasted cloud costs and basic optimization recommendations that identify likely cost drivers, unusually high projected growth, underused or oversized resources where detectable, and services that may need review.

## Actor
Registered user

## Trigger
The user has generated a manual or provider-based forecast and needs to understand the likely cost drivers.

## Outcome
The user can see forecasted costs and informational cost optimization guidance in the responsive web interface, including accessible chart/table alternatives, localized explanations, and clear insufficient-data states when an insight cannot be produced.

## Success Criteria
- The user can view forecasted cloud costs in a responsive web interface.
- The system identifies services or resources with unusually high projected cost growth where supported by available data.
- The system identifies underused or potentially oversized resources where detectable from available usage data.
- The system identifies services that may benefit from pricing or usage review.
- The system identifies forecasted cost drivers that should be investigated.
- Recommendations are informational and do not automatically change cloud resources.
- If available data is insufficient for an insight, the product explains that limitation and avoids implying certainty.
- Results, insights, insufficient-data explanations, charts/tables, and recovery guidance support English and Swedish for the initial release.

## Explicit Exclusions
- Advanced optimization recommendations such as reserved instance, savings plan, committed use, or contract purchasing guidance
- Automated remediation
- Automated cloud resource changes

## Linked Requirement IDs
- FR-CCEF-005
- FR-CCEF-006
- FR-CCEF-010  (User dashboard and home experience)
- FR-CCEF-012  (Forecast management capabilities)
- NFR-CCEF-013  (Observability and monitoring requirements)