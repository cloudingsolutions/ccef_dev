# Use Case

- Use Case ID: UC-CCEF-009
- Title: User manages privacy exports, deletion, and provider disconnect
- Product Slice ID: PS-CCEF-001
- Lifecycle State: Approved

## Summary
A registered user uses the account privacy/data controls in the responsive web application to request an account/data export, request account/data deletion, or disconnect a connected AWS, Google Cloud, or Azure provider account under the already-approved privacy, retention, deletion, export, and provider-disconnect rules.

## Actor
Registered user

## Trigger
The user wants to exercise in-scope privacy/data controls, remove provider access, recover from stale provider data, or understand what will happen to existing forecasts, alerts, provider-derived data, and audit evidence before taking a privacy or disconnect action.

## Outcome
The user can find the privacy/data controls from the authenticated account/settings experience, understand the affected data categories and consequences, confirm or cancel the selected action, and receive a localized status, completion, failure, or recovery state. Provider disconnect stops future discovery immediately, removes stored provider secrets, and causes provider-derived forecasts, insights, budget-risk alerts, anomaly flags, and monitoring states to be deleted, retained as historical/stale context, disabled, resolved, or marked stale according to PRIV-CCEF-001.

## Success Criteria
- The signed-in user can reach a dedicated privacy/data controls entry point from account/settings without leaving the registered-user web experience.
- The entry point exposes the in-scope actions for account/data export, account/data deletion, and provider disconnect only for the authenticated user's own account, provider connections, forecasts, budgets, alerts, anomaly flags, and related data objects.
- Before an export, deletion, or provider-disconnect action is submitted, the product shows a confirmation step that identifies the affected data categories at a user-understandable level, summarizes retention/deletion/export/disconnect consequences from PRIV-CCEF-001, and allows the user to cancel.
- For export requests, the user can submit the request, see status states such as received/in progress/ready/failed/partially unavailable where applicable, and receive recovery guidance without exposing raw secrets, provider credentials, or excessive provider identifiers.
- For deletion requests, the user can submit the request, see status states such as received/in progress/completed/failed/partially retained for required legal/security/audit evidence, and understand any account/session effect such as sign-out or disabled future access when account deletion completes.
- For provider disconnect, the user can disconnect an AWS, Google Cloud, or Azure connection from provider/account settings or the privacy/data controls entry point, with confirmation that stored provider secrets are removed, future discovery stops immediately, and disconnected-provider monitoring will no longer create current provider-derived budget or anomaly signals.
- After provider disconnect, prior provider-derived forecasts, insights, alerts/anomalies, and discovered-data views either remain only as labeled historical/stale context chosen or allowed under PRIV-CCEF-001, are deleted within the approved deletion window, or are resolved/disabled/marked stale when they require disconnected provider data.
- After account/data deletion, remaining product surfaces do not present deleted provider, forecast, budget, alert/anomaly, SMS, or derived data as current; legally/security-required audit evidence is minimized and not shown as active user data.
- Error and recovery states cover invalid or expired sessions, unauthorized object access, unavailable export package generation, deletion/disconnect processing failure, already-disconnected providers, stale provider data, and retry/contact-support guidance without leaking secrets or unsafe raw errors.
- Privacy export, deletion, provider-disconnect, confirmation, status, stale-data, and recovery copy is available in English and Swedish for the initial release and cannot rely on fallback strings for the critical action path.
- The privacy/data controls path remains usable and accessible at supported responsive breakpoints, with keyboard-operable controls, clear focus order, accessible confirmation dialogs, status announcements, and readable error/recovery guidance consistent with WCAG 2.2 AA targets.
- Audit evidence records export, deletion, provider-disconnect, status, and recovery outcomes at a minimized non-secret level consistent with PRIV-CCEF-001.

## Explicit Exclusions
- Privacy/compliance regimes beyond the approved initial GDPR baseline unless separately defined.
- Legal advice content for users.
- Provider-side cloud resource deletion or remediation.
- Team, organization, or administrator-driven data subject request workflows beyond the registered-user path.
- Exporting raw provider credentials, authentication secrets, or security-sensitive internals.

## Linked Requirement IDs
- PRI-CCEF-003
- PRI-CCEF-009
- FR-CCEF-010  (User dashboard and home experience)
- FR-CCEF-011  (Provider connection management)
- FR-CCEF-012  (Forecast management capabilities)
- NFR-CCEF-013  (Observability and monitoring requirements)