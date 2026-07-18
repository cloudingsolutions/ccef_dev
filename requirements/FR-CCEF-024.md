# Requirement

- Requirement ID: FR-CCEF-024
- Title: User can view current account information
- Requirement Type: functional
- Product Slice IDs: PS-CCEF-001
- Lifecycle State: Approved

## Requirement Statement
The system shall display the authenticated user's current account information including name, email, and language preference when they access the account settings page.

## Rationale
Users need to see their current account information before making any changes to ensure they are modifying the correct account and to understand what information is currently stored.

## Acceptance Criteria
- Given the user is authenticated and navigates to the account settings page
- When the account settings page loads
- Then the system shall display the user's current display name
- And the system shall display the user's email address
- And the system shall display the user's current language preference (English or Swedish)

## Explicit Exclusions
This requirement does not include:
- Displaying advanced profile information (bio, profile picture, etc.)
- Displaying social media connections
- Displaying payment or billing information
- Displaying provider connection details

## Constraints
- The display name must be shown exactly as stored in the system (no modification for display purposes)
- Email address should be displayed but may be partially masked for security (e.g., j**n@e***.com)
- Language preference must be displayed as the full language name (English/Svenska) not just codes
- Information must be retrieved from the user's account record in the database
- No external API calls should be made to retrieve this information

## Validation Method
- automated test
- manual QA
- code review

## References
- Related Requirements, non-blocking: FR-CCEF-025, FR-CCEF-026, FR-CCEF-027
- ADRs:
- API / Data Contracts: GET /api/v1/account/profile endpoint
- Policies / Regulations:
- Design Artifacts: Account settings UI mockups
- Other:

## Traceability
- Product Slices: PS-CCEF-001
- Use Cases: UC-CCEF-006