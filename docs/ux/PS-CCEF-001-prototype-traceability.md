# PS-CCEF-001 Prototype Traceability And Scope Map

- Product ID: CCEF
- Product Slice ID: PS-CCEF-001
- Prototype Revision ID: UXPROTO-CCEF-001
- Source Repository: `/Users/wolney/repos/projects/ccef-ui-ux`
- Source Path: `prototype/index.html`
- Source Commit: `042b05cfa0c9664eb542ca922ba69be537ec5ad2`
- Source Branch At Capture: `main`
- Source File Blob: `5f34d27603c2b438a903f9b05f6eaa5f4b18d435`
- Source Repo State At Capture: Clean
- Related UX Reference: `product/docs/ux/PS-CCEF-001-prototype-ux-reference.md`
- Prototype Registry: `product/docs/ux/prototype-registry.md`
- Reference State: Draft traceability input

## Purpose

This document maps the current UX/UI prototype to product artifacts so downstream agents can see how the prototype should trickle into the product structure.

The prototype should be used as a source of UX evidence. It should not bypass approved slice, use case, requirement, ADR, milestone, task, or work item artifacts.

## Downstream Agent Expectations

Downstream agents are expected to have access to UX prototype revision `UXPROTO-CCEF-001` when designing or implementing PS-CCEF-001 user-facing work.

For prototype-defined screens and states, agents must inspect the pinned HTML prototype revision and preserve its look and feel. The product documents define scope and traceability; the pinned prototype revision defines the intended visual and interaction treatment for the screens it covers.

Agents may make reasonable design guesses only for screens, components, or states that are not defined in the prototype. Those guesses must extend the prototype's established design language and should be marked as extrapolated UX when they affect product behavior or acceptance.

If an agent cannot access the prototype file, it should treat that as a blocker for prototype-defined UI work rather than inventing a replacement look and feel.

Work items that depend on prototype-defined UI should carry the prototype revision ID and commit SHA, for example:

```text
UX Prototype Revision: UXPROTO-CCEF-001
UX Prototype Repository: /Users/wolney/repos/projects/ccef-ui-ux
UX Prototype Path: prototype/index.html
UX Prototype Commit: 042b05cfa0c9664eb542ca922ba69be537ec5ad2
UX Prototype Use: Visual authority for defined screens and states
```

## Traceability Map

| Prototype Area | PS-CCEF-001 Disposition | Product Artifact Targets |
|---|---|---|
| First-visit authentication gate | In scope | Slice success criteria; UC-CCEF-001; UC-CCEF-003; FR-CCEF-001; FR-CCEF-002; FR-CCEF-003 |
| Sign in with Google | In scope for authentication behavior | UC-CCEF-001; FR-CCEF-001; NFR-CCEF-001; NFR-CCEF-002; NFR-CCEF-003; NFR-CCEF-004 |
| Sign in with Apple | In scope for authentication behavior | UC-CCEF-001; FR-CCEF-002; NFR-CCEF-001; NFR-CCEF-002; NFR-CCEF-003; NFR-CCEF-004 |
| Email one-time code sign-in | In scope | UC-CCEF-003; FR-CCEF-003; FR-CCEF-011; FR-CCEF-012; NFR-CCEF-002; NFR-CCEF-003 |
| Email one-time code account creation | In scope | UC-CCEF-003; FR-CCEF-003; FR-CCEF-009; FR-CCEF-011; FR-CCEF-012; FR-CCEF-015 |
| Terms and privacy checkbox gate | In scope | Slice success criteria; FR-CCEF-006; FR-CCEF-031; NFR-CCEF-005; NFR-CCEF-009 |
| Terms and privacy document modal | In scope as acceptance UX, copy requires legal review | FR-CCEF-006; FR-CCEF-031; product/docs/privacy/data-handling-policy.md |
| Language selection during signup | In scope if product confirms signup timing | UC-CCEF-006; FR-CCEF-022; FR-CCEF-023; NFR-CCEF-008 |
| Detected language message | In scope | Slice success criteria; FR-CCEF-022; FR-CCEF-023; NFR-CCEF-008 |
| Data residency notice during signup | In scope | UC-CCEF-008; FR-CCEF-032; ADR-0002; product/docs/privacy/data-handling-policy.md |
| User-initiated residency change | In scope if legally permitted | UC-CCEF-008; FR-CCEF-032; ADR-0002 |
| Phone number collection | In scope, but timing conflict must be resolved | UC-CCEF-004; FR-CCEF-018; FR-CCEF-019; FR-CCEF-020; FR-CCEF-021 |
| SMS verification code | In scope | UC-CCEF-004; FR-CCEF-018; FR-CCEF-019; FR-CCEF-021; NFR-CCEF-003 |
| Skip phone for now | Product decision needed | Slice success criteria; UC-CCEF-004; FR-CCEF-020 |
| Account settings profile tab | In scope for basic account management | UC-CCEF-005; UC-CCEF-006; UC-CCEF-008; FR-CCEF-024 through FR-CCEF-030; FR-CCEF-032 |
| Privacy and data settings tab | Partly in scope, partly compliance expansion | UC-CCEF-007; UC-CCEF-008; FR-CCEF-031; FR-CCEF-032; NFR-CCEF-005; ADR-0002 |
| Notification settings tab | In scope only where tied to SMS consent/contact preferences | UC-CCEF-004; FR-CCEF-020; FR-CCEF-021 |
| Empty app states after skipped setup | In scope as post-auth landing behavior only | Slice success criteria; milestone demo criteria |
| Environment setup wizard | Future context | Future cloud account/environment setup slice |
| Cloud provider connection | Future context | Future provider integration slice; future ADRs |
| Provider comparison and cost analysis UI | Future context | Future comparison/forecasting slices |
| Budgets, alerts, forecast, waste, exports | Future context except alert consent copy | Future cost control and forecasting slices |
| Plans and billing | Explicitly excluded or deferred | Future subscription/billing slice |

## Downstream Artifact Flow

Use the prototype information in this order:

1. Resolve `UXPROTO-CCEF-001` through `product/docs/ux/prototype-registry.md`.
2. Inspect the pinned prototype revision for any prototype-defined screen or state.
3. Update or confirm `product/slices/PS-CCEF-001/slice.md` for user-visible behavior, constraints, explicit exclusions, and deferred context.
4. Update use cases for journey timing, alternate paths, user-visible states, and expected confirmations.
5. Update requirements for exact acceptance criteria, validation behavior, accessibility obligations, and user-facing error states.
6. Update ADRs only when a product-facing UX decision forces an architectural decision, such as residency selection, consent evidence, session/token handling, or localization architecture.
7. Update milestones with demo criteria and feature flags after slice, use cases, and requirements are consistent.
8. Derive tasks and work items only after the above artifacts agree.
9. Derive QA cases from approved requirements and milestone demo criteria, using the prototype as supporting evidence.

## Conflicts And Refinement Questions

### Phone Collection Timing

The prototype places phone collection immediately after account creation and before first-run setup. Current use-case text says phone number collection during initial account creation is excluded or handled separately.

Recommended resolution: decide whether phone collection is part of the required account creation completion path, a skippable post-account step, or a later settings-only action. Then update UC-CCEF-004, FR-CCEF-018 through FR-CCEF-021, and milestone scope accordingly.

### Language Timing

The prototype collects language during signup and also exposes language in settings. Some artifact text says language preference is handled in post-onboarding.

Recommended resolution: make device-language detection and default selection part of account creation/onboarding, and make later changes part of account settings. Then align UC-CCEF-006, FR-CCEF-022, FR-CCEF-023, and the slice success criteria.

### Supported Languages

The slice constrains the release to English and Swedish, but the prototype settings list additional languages.

Recommended resolution: keep only English and Swedish as PS-CCEF-001 acceptance scope. Treat other language names in the prototype as future-language UI placeholders unless the slice is intentionally expanded.

### Password Language

The prototype explicitly uses passwordless account creation and settings text says no password is used. Any product artifact that requires password update or password management conflicts with the prototype direction.

Recommended resolution: decide whether PS-CCEF-001 is passwordless-only. If yes, remove or defer password-update commitments from slice, use cases, requirements, and milestones.

### SMS Consent Versus SMS 2FA

The prototype mixes SMS alerts and "Two-factor authentication (SMS) Coming soon" in settings.

Recommended resolution: keep SMS alert consent and verified phone management in PS-CCEF-001 only if needed for this slice. Keep SMS 2FA explicitly future unless a requirement is added.

### Legal Copy

The prototype Terms and Privacy modal copy includes cloud-provider read-only access and usage metadata collection, which belong more naturally to future cloud-account connection slices.

Recommended resolution: keep account creation terms/privacy acceptance in PS-CCEF-001, but do not treat the prototype modal body as final legal copy for cloud-provider integrations.

### Auth Error States

The prototype shows happy-path flows, resend confirmations, validation hints, and disabled consent actions, but does not define failure states for OAuth denial, token callback errors, invalid or expired codes, network timeouts, account conflicts, rate limits, or unsupported residency.

Recommended resolution: add explicit user-facing error states to the relevant use cases and requirements before implementation work is generated.

## Proposed Product Artifact Updates

### Slice

Add a short UX reference section to `product/slices/PS-CCEF-001/slice.md` pointing to:

- `product/docs/ux/PS-CCEF-001-prototype-ux-reference.md`
- `product/docs/ux/PS-CCEF-001-prototype-traceability.md`

Use the section to state that these documents are design evidence, not direct implementation scope.

### Use Cases

Refine:

- UC-CCEF-001 for SSO terms gate, post-signup phone step, and user-visible OAuth failure states.
- UC-CCEF-003 for email code screen behavior, code expiration, resend, use-different-email, invalid/expired code, and rate limit states.
- UC-CCEF-004 for phone timing, skip behavior, SMS consent timing, resend, use-different-number, invalid/expired code, and rate limit states.
- UC-CCEF-006 for language timing, device detection, confirmation, override, and settings change.
- UC-CCEF-007 for privacy/data settings states if data export and deletion remain in slice.
- UC-CCEF-008 for detected residency, user-changeable EU regions, unsupported or indeterminate residency handling.

### Requirements

Refine acceptance criteria where necessary:

- FR-CCEF-001 and FR-CCEF-002: SSO sign-up terms gate and provider failure states.
- FR-CCEF-003, FR-CCEF-011, and FR-CCEF-012: email OTP entry, expiration, resend, invalid code, expired code, and rate limit UX.
- FR-CCEF-018 through FR-CCEF-021: phone collection timing, verification, skip, resend, consent, settings update, and removal.
- FR-CCEF-022 and FR-CCEF-023: detected language and language override.
- FR-CCEF-031 and FR-CCEF-032: terms/privacy acceptance and data residency UX.
- NFR-CCEF-008: modal, toast, OTP, tab, toggle, and form accessibility.

### Milestones

Milestone demo criteria should reference product-approved behavior, not the prototype directly. The prototype should be used to clarify:

- whether phone verification is in Milestone 1 or Milestone 2;
- whether language/residency appears in account creation or later onboarding;
- whether skipped setup is a PS-CCEF-001 demo requirement;
- which error states are expected in each milestone demo.

## Non-Goals For PS-CCEF-001

Do not create PS-CCEF-001 work items for:

- provider credential collection;
- AWS, Azure, or Google Cloud account discovery;
- environment service catalog;
- cost comparison, forecast, waste detection, budgets, alerts, or exports;
- billing plans, checkout, or subscription changes;
- imported cost history or read-only cloud usage metadata;
- recommendation calculations.

These are visible in the prototype but belong to future slices unless the product slice is explicitly expanded.
