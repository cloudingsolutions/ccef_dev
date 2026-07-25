# PS-CCEF-001 Prototype UX Reference

- Product ID: CCEF
- Product Slice ID: PS-CCEF-001
- Prototype Revision ID: UXPROTO-CCEF-001
- Source Repository: `/Users/wolney/repos/projects/ccef-ui-ux`
- Source Path: `prototype/index.html`
- Source Commit: `042b05cfa0c9664eb542ca922ba69be537ec5ad2`
- Source Branch At Capture: `main`
- Source File Blob: `5f34d27603c2b438a903f9b05f6eaa5f4b18d435`
- Source Repo State At Capture: Clean
- Source Artifact Type: Interactive single-file HTML prototype
- Prototype Registry: `product/docs/ux/prototype-registry.md`
- Reference State: Draft UX reference input

## Purpose

This document captures the PS-CCEF-001 user experience information that can be extracted from the current Clouding UX/UI prototype.

The prototype is useful design evidence, but it is not itself the canonical product specification. Product commitments become canonical only when they are represented in approved product slice, use case, requirement, architectural decision, milestone, task, or work item artifacts.

## Visual Design Authority

For screens, components, states, and flows represented in UX prototype revision `UXPROTO-CCEF-001`, downstream design and implementation agents must inspect and follow the prototype for look and feel.

This includes layout density, navigation structure, typography scale, spacing, card/table/tabs/modal patterns, button hierarchy, icons, form styling, empty states, toast behavior, and account/settings interaction patterns.

Agents must not invent a different visual direction for prototype-defined screens. If implementation constraints require deviation, the deviation must be called out as a product/design gap before work proceeds.

For screens or states not represented in the prototype, agents may extrapolate, but the extrapolation must stay consistent with the prototype's established design language and must not introduce a competing product style.

## Interpretation Rules

- Treat this document as product-facing UX source material for PS-CCEF-001 refinement.
- Treat `UXPROTO-CCEF-001` as the visual authority for any screen or state it already defines.
- Resolve `UXPROTO-CCEF-001` through `product/docs/ux/prototype-registry.md`, using the pinned repository, path, and commit.
- Treat exact prototype copy as candidate product copy, not final legal, security, or compliance copy.
- Treat prototype navigation, enabled/disabled states, modals, and empty states as intended interaction guidance unless contradicted by approved requirements.
- Do not derive implementation work from prototype screens that are marked future context or out of scope for PS-CCEF-001.
- Do not replace the prototype's look and feel with a new design system or alternate visual style for defined screens.
- For undefined screens or missing states, extend the prototype's existing patterns rather than starting from a new design direction.
- When this document conflicts with an approved use case or requirement, record the conflict and resolve it through product artifact refinement before implementation.

## Safe Prototype Access

Agents should inspect the pinned prototype revision without disturbing the active UX repository checkout.

Read-only inspection:

```bash
git -C /Users/wolney/repos/projects/ccef-ui-ux show 042b05cfa0c9664eb542ca922ba69be537ec5ad2:prototype/index.html
```

Browser/manual inspection:

```bash
git -C /Users/wolney/repos/projects/ccef-ui-ux worktree add /tmp/ccef-ui-ux-042b05c 042b05cfa0c9664eb542ca922ba69be537ec5ad2
```

Then inspect:

```text
/tmp/ccef-ui-ux-042b05c/prototype/index.html
```

Do not run `git checkout 042b05cfa0c9664eb542ca922ba69be537ec5ad2` in `/Users/wolney/repos/projects/ccef-ui-ux` unless that repository is clean and the task explicitly allows moving the active working copy.

## In Scope For PS-CCEF-001

The following prototype areas are relevant to User Access and Account Management Foundation:

- First-visit authentication gate.
- Sign-in with Google SSO, Apple SSO, or email one-time code.
- Account creation with Google SSO, Apple SSO, or email one-time code.
- Terms of Service and Privacy Policy acceptance before account creation.
- Explicit checkbox gate before enabling the Create account or Agree and continue action.
- Email one-time code entry, resend action, and use-different-email action.
- Phone number collection, SMS verification code entry, resend action, use-different-number action, and skip-for-now action.
- Language selection during onboarding, including device-detected default language messaging.
- Data residency display during onboarding, including detected EU Stockholm default and user-initiated region change.
- Account settings for name, work email, sign-in method, mobile number, language, data residency, and contact preferences.
- Privacy and data settings for region, language, consent toggles, data export request, and account deletion entry point.
- Notification settings for alert types, SMS contacts, contact verification state, and default snooze duration.
- Empty post-authentication states when setup is skipped.

## Future Context Not In Scope For PS-CCEF-001

The prototype includes complete app-shell flows that should be preserved as future product context but must not become PS-CCEF-001 acceptance criteria:

- Cloud account connection for AWS, Azure, and Google Cloud.
- Environment setup wizard for business type, provider, region, target budget, and service catalog.
- Provider comparison, comparison engine loading, savings breakdown, and cost drilldowns.
- Forecasting, waste detection, budgets, alert rules, anomaly investigation, and exports.
- Plans, billing, subscription management, checkout, and cloud spend under management.
- Read-only cloud provider credential collection and 90-day cost import.
- Cross-provider service catalog and provider-specific service names.
- Recommendation, savings, waste, and forecast calculations.

For PS-CCEF-001, these screens should only influence the post-authentication destination and empty-state behavior. They should otherwise remain deferred or adjacent product intent.

## Primary User Journeys

### Returning User Signs In

1. User lands on the authentication gate.
2. Screen title is "Welcome back" with supporting copy "Sign in to your Clouding workspace".
3. User can choose Continue with Google, Continue with Apple, or email one-time code.
4. If SSO is selected in sign-in mode, the prototype enters the app directly.
5. If email is selected, the user enters a work email and requests a sign-in code.
6. The user enters a six-digit code, can request a resend, or can use a different email.
7. Successful verification enters the app.

### New User Creates Account With SSO

1. User switches from sign-in to Create your account.
2. User selects Continue with Google or Continue with Apple.
3. Before account creation completes, the prototype shows a blocking terms gate titled "One thing before we start".
4. The primary action remains disabled until the user explicitly checks agreement to Terms of Service and Privacy Policy.
5. After agreement, the user is asked to add a mobile number.
6. User may enter a mobile number and request an SMS verification code, or skip for now.
7. If phone is entered, the user enters a six-digit SMS code, can resend the code, or can use a different number.
8. Completion starts the first-run setup wizard.

### New User Creates Account With Email Code

1. User opens Create your account.
2. User sees SSO options plus fields for full name, work email, language, data residency, and terms acceptance.
3. Language default is presented as "English - detected from your device" with Swedish as an alternate option.
4. Data residency is presented as "EU - Stockholm", detected from location, with a Change region action.
5. Changing region reveals selectable EU regions: Stockholm, Frankfurt, and Ireland.
6. The prototype explicitly states that no password is created and a six-digit email code will confirm the account.
7. Create account remains disabled until the terms/privacy checkbox is selected.
8. After submission, the user enters the six-digit email code, can resend the code, or can use a different email.
9. Successful email verification proceeds to mobile number add/verify or skip.
10. Completion starts the first-run setup wizard.

### User Skips Initial Setup

1. During first-run setup, the user can choose Skip setup for now.
2. The prototype shows a confirmation modal titled "Skip setup for now?".
3. User can continue setup or continue to Clouding.
4. Continuing to Clouding enters an empty app mode with add-first-environment calls to action.

For PS-CCEF-001, this confirms that authentication can complete without cloud-provider setup. The environment setup itself remains outside the slice.

### User Manages Account Settings

1. The app shell account menu exposes Account settings and Sign out.
2. The Account settings page includes tabs for Account, Connected accounts, Notifications, Privacy and data, and Billing.
3. PS-CCEF-001-relevant tabs are Account, Notifications, and Privacy and data.
4. Account tab includes full name, work email, default language, data residency, sign-in method, mobile number, SMS 2FA coming-soon status, and contact preferences.
5. Privacy and data tab includes data residency, interface language, consent toggles, data export request, and account deletion entry point.
6. Notifications tab includes alert type toggles, SMS contacts, add/remove contact behavior, verification state, and snooze duration.

Connected accounts and Billing are future context for later slices.

## UX States And Behaviors

### Blocking Consent

- Create account is disabled until Terms of Service and Privacy Policy agreement is checked.
- Agree and continue is disabled until Terms of Service and Privacy Policy agreement is checked for SSO sign-up.
- Terms and Privacy links open a document modal without leaving the flow.

### One-Time Code Entry

- Email and SMS code screens show six separate one-character numeric inputs.
- Code screens provide a Continue action, a Resend code action, and a route to change the email or phone number.
- Prototype code text says email codes expire in 10 minutes.
- Resend actions produce toast confirmation.

### Phone Verification

- Phone collection happens after account creation/authentication path selection and before first-run setup.
- Phone collection is positioned as enabling urgent cost alerts by text.
- User can skip phone setup.
- If phone is provided, it must be verified before completion.

### Language And Residency

- Signup shows detected language and allows user override.
- Signup shows detected account data region and allows explicit region selection.
- Settings allows later language and residency changes.
- The prototype shows additional language options in settings beyond English and Swedish; PS-CCEF-001 should keep the approved slice constraint unless explicitly refined.

### Empty States

- If setup is skipped, Overview, Environments, Waste detection, Budgets, Alerts, Providers, and Forecast show empty states.
- Empty states consistently explain what is missing and provide an Add environment action.
- For PS-CCEF-001, the important behavior is that users can reach an authenticated product shell without provider setup.

### Toasts And Status Feedback

- Resend code, account updates, contact actions, snooze changes, and similar actions use transient toast feedback.
- Toasts include title, optional supporting text, icon, close action, and auto-dismiss.
- Implementation should ensure status feedback is accessible through ARIA live regions per NFR-CCEF-008.

## Candidate Product Copy

The following strings are product-significant candidate copy from the prototype:

- "Welcome back"
- "Sign in to your Clouding workspace"
- "Create your account"
- "See what your cloud should cost on every major provider."
- "Continue with Google"
- "Continue with Apple"
- "Work email"
- "Email me a sign-in code"
- "No password needed. We'll send a 6-digit code to your inbox."
- "No password to create. We'll email you a 6-digit code to confirm it's you."
- "Check your email"
- "Enter the 6-digit code we sent to [email]. It expires in 10 minutes."
- "Resend code"
- "Use a different email"
- "One thing before we start"
- "Please review and accept our terms to create your Clouding account."
- "I agree to Clouding's Terms of Service and Privacy Policy."
- "Add your mobile number"
- "Urgent cost alerts can reach you by text, our fastest channel. You can add more contacts later in Settings."
- "Text me a verification code"
- "Skip for now"
- "Verify your number"
- "Enter the 6-digit code we just texted to [phone]."
- "Use a different number"
- "Your account data is stored in EU - Stockholm, detected from your location. GDPR compliant."
- "You can change this anytime in Settings."

Final copy must be reviewed for brand naming, legal accuracy, localization, accessibility, and security clarity.

## Accessibility And Usability Notes

Implementation derived from this prototype must satisfy NFR-CCEF-008. The prototype implies the following UX checks:

- Every form field needs a programmatic label and visible focus state.
- SSO buttons, terms links, checkboxes, select controls, code boxes, modal controls, tabs, toggles, and toast dismissal must be keyboard operable.
- Modals must trap focus while open and return focus to the triggering control when closed.
- Disabled primary actions must expose their disabled state programmatically.
- OTP inputs must support paste, correction, screen reader labels, and a non-fragmented accessible name.
- Toasts and validation hints must be announced through ARIA live regions.
- Language changes must update page language metadata and be announced.
- Error states must identify the field or operation that failed and describe recovery.
- Color must not be the only cue for selected, verified, high severity, pending, or disabled states.
- The layout must remain usable at mobile, tablet, small desktop, and desktop breakpoints.

## Product Gaps To Resolve Before Implementation

- The prototype is a happy-path reference; approved use cases and requirements define provider denial, provider callback failure, network failure, expired/incorrect OTP, rate limiting, account conflict, and unsupported residency error behavior.
- Phone collection is optional after account creation and before first-run setup; users can skip it and complete SMS setup later from account settings.
- Language selection is part of onboarding after account creation and remains changeable later in account settings.
- The prototype settings list languages beyond the currently approved English and Swedish scope.
- The prototype uses Clouding brand copy, while the product artifacts identify the product as CCEF and Cloud Cost Estimator and Forecaster.
- The prototype includes account deletion and data export entry points in settings; scope must confirm whether these are PS-CCEF-001 commitments or future compliance/account-management items.
