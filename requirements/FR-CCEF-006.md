Requirement ID: FR-CCEF-006
Title: Basic cost optimization recommendations
Requirement Type: functional
Product Slice IDs: PS-CCEF-001
Lifecycle State: Approved

# Requirement Statement
The system shall provide informational basic cost optimization insights such as services or resources with unusually high projected cost growth, underused or potentially oversized resources detectable from available usage data, services that may benefit from pricing or usage review, and forecasted cost drivers that should be investigated. These recommendations shall be informational and not automatically change cloud resources.

# Rationale
This requirement ensures users receive actionable insights to help optimize their cloud spending without the system making automatic changes to their infrastructure, maintaining user control.

# Acceptance Criteria
- Given a user has generated a cloud cost forecast (manual or provider-based)
- When viewing the forecast results
- Then the system shall provide informational basic cost optimization insights including:
  * Services or resources with unusually high projected cost growth (>20% month-over-month increase)
  * Underused or potentially oversized resources (<20% utilization for compute resources, where detectable from available usage data)
  * Services that may benefit from pricing or usage review (showing consistent underutilization over 30-day period)
  * Forecasted cost drivers that should be investigated (top 5 services by projected cost)
- And these recommendations shall be informational and shall not automatically change cloud resources
- Given insufficient data exists for specific optimization insights (less than 7 days of data)
- When generating recommendations
- Then the system shall provide clear insufficient-data explanations with suggestions for minimum data collection period
- And the system shall log all optimization insights generated for audit and improvement purposes
- And the system shall provide a confidence level (high/medium/low) for each insight based on data quality and quantity

# Explicit Exclusions
- Advanced optimization recommendations such as reserved instance, savings plan, committed use, or contract purchasing guidance
- Automated cloud resource changes
- Automated remediation of cost issues
- Guaranteed cost savings from following recommendations

# Constraints
- The system provides informational basic cost optimization insights with the following defined thresholds:
  * Unusually high growth: >20% month-over-month increase in projected cost
  * Underused resources: <20% utilization for compute instances over 7-day period
  * Oversized resources: consistently >80% utilization but <20% utilization for burstable instances
  * Services for review: showing <15% utilization for 30+ consecutive days
- These recommendations are informational and do not automatically change cloud resources
- The system shall log optimization insight generation events for observability and improvement tracking
- Insight algorithms shall be deterministic enough for test oracles with consistent outputs given identical inputs
- For test oracle purposes, the system shall consistently apply these thresholds to generate optimization insights

# Validation Method
- automated test
- manual QA
- code review

# References
- Related Requirements, non-blocking:
- ADRs:
- API / Data Contracts:
- Policies / Regulations:
- Design Artifacts:
- Other:

# Traceability
- Product Slices: PS-CCEF-001
- Use Cases: UC-CCEF-003, UC-CCEF-005, UC-CCEF-006
