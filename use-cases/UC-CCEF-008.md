# Use Case

- Use Case ID: UC-CCEF-008
- Title: User receives simple anomaly flags for unusual cost or usage patterns
- Product Slice ID: PS-CCEF-001
- Lifecycle State: Approved

## Summary
A registered user sees simple anomaly flags when cost or usage patterns appear unusual based on historical usage, forecast expectations, or benchmark assumptions, with SMS alerts available when enabled.

## Actor
Registered user

## Trigger
The user's actual, discovered, or forecasted cloud cost or usage pattern appears unusual against available comparison signals.

## Outcome
The user can identify unusual patterns in the product and receive SMS alerts for anomaly conditions when SMS alerts are enabled with the required phone number, verification, consent, and opt-out state.

## Success Criteria
- The system can flag unusual cost or usage patterns based on historical usage where minimum comparable data is available.
- The system can flag unusual cost or usage patterns based on forecast expectations.
- The system can flag unusual cost or usage patterns based on benchmark assumptions and labels benchmark-based flags clearly.
- The user can see simple anomaly flags in the product experience.
- Anomaly lifecycle, deduping, threshold, minimum-data, and SMS handoff behavior follow deterministic rules.
- Insufficient anomaly data states do not fabricate flags and explain recovery or waiting conditions.
- The user can receive SMS alerts for anomaly conditions when SMS alerts are enabled.
- The product requires an available phone number before SMS anomaly alerts can be enabled.
- The product verifies the phone number at a high level before sending SMS anomaly alerts.
- The product captures or respects user consent for SMS alert delivery before sending SMS anomaly alerts.

## Explicit Exclusions
- Advanced anomaly investigation workflows
- Automated remediation
- Alert delivery channels other than in-app/dashboard notifications and SMS unless separately defined

## Linked Requirement IDs
- FR-CCEF-007
- FR-CCEF-010  (User dashboard and home experience)
- FR-CCEF-011  (Provider connection management)
- FR-CCEF-012  (Forecast management capabilities)
- NFR-CCEF-013  (Observability and monitoring requirements)