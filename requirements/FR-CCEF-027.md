# Requirement

- Requirement ID: FR-CCEF-027
- Title: User can manage basic contact preferences
- Requirement Type: functional
- Product Slice IDs: PS-CCEF-001
- Lifecycle State: Approved

## Requirement Statement
The system shall allow authenticated users to manage their basic contact preferences, specifically email notification settings for different types of system communications.

## Rationale
Users need control over what types of communications they receive from the system to reduce notification fatigue while ensuring they get important information.

## Acceptance Criteria
- Given the user is authenticated and viewing their account settings
- When the user navigates to the contact preferences section
- Then the system shall display toggle switches for at least these notification types:
  * Weekly cost summary emails
  * Alert notifications for cost thresholds
  * Monthly usage reports
  * System maintenance notifications
- Given the user toggles a notification setting and saves the change
- Then the system shall save the new preference to the user's account
- And the system shall display a confirmation message that preferences have been updated
- Given the user disables a notification type
- When the system would normally send that type of notification
- Then the system shall not send the notification to that user
- Given the user enables a notification type
- When the system would normally send that type of notification
- Then the system shall send the notification to that user according to the scheduled timing

## Explicit Exclusions
This requirement does not include:
- SMS or push notification preferences
- Custom notification frequency settings
- Advanced filtering of notifications (by project, cost center, etc.)
- Unsubscribing from all emails (must be done via privacy/request deletion flow)
- Third-party marketing or promotional communications
- Real-time notification preferences (in-app notifications, etc.)

## Constraints
- Notification preferences must be stored as boolean values (enabled/disabled)
- System must respect user preferences when generating and sending notifications
- Default notification preferences should be sensible (enable critical alerts, disable less critical by default)
- Changing notification preferences must be logged in the audit trail
- System must prevent overriding user preferences through administrative interfaces without explicit consent
- Notification types must be clearly labeled with descriptions of what they include

## Validation Method
- automated test
- manual QA
- code review

## References
- Related Requirements, non-blocking: FR-CCEF-024, FR-CCEF-025, FR-CCEF-026
- ADRs:
- API / Data Contracts: PATCH /api/v1/account/notifications endpoint
- Policies / Regulations: CAN-SPAM Act, GDPR (for electronic communications)
- Design Artifacts: Account settings UI mockups
- Other: Email template specifications

## Traceability
- Product Slices: PS-CCEF-001
- Use Cases: UC-CCEF-006