# Use Case

- Use Case ID: UC-CCEF-007
- Title: User configures budget thresholds and receives budget-risk alerts
- Product Slice ID: PS-CCEF-001
- Lifecycle State: Approved

## Summary
A registered user defines budget thresholds for forecasted or actual cloud costs, sees in-app/dashboard budget-risk alerts, and can enable SMS budget-risk alerts when a phone number is available, verified, and consented for alert delivery.

## Actor
Registered user

## Trigger
The user wants to be warned when cloud costs may exceed budget expectations.

## Outcome
The user can configure budget thresholds, see deduplicated budget-risk alerts in the product, and receive SMS alerts for budget-risk conditions when SMS alerts are enabled with the required phone number, verification, consent, and opt-out state.

## Success Criteria
- The user can configure budget thresholds.
- The system can alert the user when forecasted costs meet or exceed a configured threshold.
- The system can alert the user when actual or discovered usage meets or exceeds a configured threshold.
- The user can see budget-risk alerts in-app or on the dashboard.
- Budget-risk alert lifecycle, deduping, and SMS handoff behavior follow deterministic rules.
- The user can enable SMS alerts for budget-risk conditions within the basic alert preferences supported by the initial production scope.
- The product requires an available phone number before SMS budget-risk alerts can be enabled.
- The product verifies the phone number at a high level before sending SMS budget-risk alerts.
- The product captures or respects user consent for SMS alert delivery before sending SMS budget-risk alerts.
- Missing phone, pending verification, absent/withdrawn consent, opt-out, and insufficient budget-risk data states provide clear recovery guidance.
- The user can receive SMS alerts for budget-risk conditions when SMS alerts are enabled and phone number, verification, and consent requirements are satisfied.

## Explicit Exclusions
- Alert delivery channels other than in-app/dashboard notifications and SMS unless separately defined
- Complex FinOps workflows or approval flows
- Chargeback/showback reporting
- Advanced notification workflows, schedules, routing rules, or organization/team alert policies

## Linked Requirement IDs
- FR-CCEF-007
- FR-CCEF-010  (User dashboard and home experience)
- FR-CCEF-011  (Provider connection management)
- FR-CCEF-012  (Forecast management capabilities)
- NFR-CCEF-013  (Observability and monitoring requirements)