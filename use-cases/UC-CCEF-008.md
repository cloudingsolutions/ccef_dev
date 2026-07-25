# Use Case

- Use Case ID: UC-CCEF-008
- Title: User confirms or selects data residency region
- Product Slice IDs: PS-CCEF-001
- Lifecycle State: Approved

## Summary
During onboarding, the system infers the user's data residency region from IP address, with Europe as the minimum supported region, and allows users to select an alternative region where legally permitted.

## Actor
User completing the onboarding flow after account creation but before accessing core functionality

## Trigger
User reaches the data residency confirmation step in the onboarding flow

## Outcome
User's data residency region is established and recorded, either through system inference or user selection where permitted

## Success Criteria
1. System attempts to infer residency from IP address
2. When inference is confident and region is supported, system pre-selects that region
3. When inference fails or region is unsupported, system prompts user to select region
4. Europe is presented as the minimum supported residency region
5. Users can select another supported region where regulation permits choice
6. System clearly indicates when residency is inferred vs. user-selected
7. System prevents selection of unsupported regions with clear explanation
8. System does not silently assign users to arbitrary regions when residency cannot be determined
9. Selected or inferred residency is recorded with timestamp and user ID
10. System provides explanation of what data residency means for the user
11. User can view their recorded residency in account settings (but not change it after onboarding)
12. System handles edge cases like VPNs, proxies, and mobile roaming appropriately
13. Residency determination attempts and outcomes are recorded in the audit trail
14. If the inferred region is unsupported, the system explains why the region is not available and requires the user to select a supported region
15. If residency cannot be confidently inferred, the system presents manual selection without silently assigning an arbitrary region

## Explicit Exclusions
- Data residency options beyond those explicitly supported by the system
- Automatic residency changes based on detected location changes
- Requiring residency selection to complete initial account creation; residency confirmation occurs during onboarding
- Ability to change residency after initial onboarding completion
- Residency-based feature flags or conditional functionality
- Data partitioning or sharding based on residency
- Legal advice or interpretation of residency regulations
- Integration with external residency verification services
- Residency confirmation via government ID or documentation

## Linked Requirement IDs
- FR-CCEF-032
