# Architectural Decision Record

- ADR ID: ADR-0001
- Title: Modular Monolith with Clear Boundaries (Path to Microservices) Approach
- Status: Approved
- Product Slice IDs: PS-CCEF-001
- Related Requirement IDs: 
- Related Milestone IDs:
- Decision: Adopt a modular monolith architecture with clear boundaries that provides a path to microservices extraction when needed, rather than starting with a distributed system or monorepo of independent services.
- Context: 
  We need to balance production readiness with avoiding over-engineering for the CCEF MVP. The system must be cloud provider agnostic, built with Node/TypeScript, and support lane-based work with specialized agents (backend-coder, frontend-coder, database-coder, etc.). We need atomic, lane-validatable work items that enable parallel development while maintaining system integrity.
  
  The architecture must support:
  - Clear separation of concerns aligned with team lanes
  - Evolutionary path to microservices if scaling demands it
  - Production-ready background processing for forecast/alerting needs
  - GDPR-compliant data handling foundations
  - Prevention of scope creep through explicit boundaries
- Options Considered:
  1. **Distributed Microservices from Day One**: Multiple independently deployable services with their own CI/CD pipelines
  2. **Monorepo of Independent Services**: Single repository but separate deployable units (api/, web/, worker/ folders)
  3. **Big Ball of Mud Monolith**: No enforced boundaries, everything coupled together
  4. **Modular Monolith with Clear Boundaries (Chosen)**: Single deployable unit with internal modules having explicit interfaces and lane-aligned ownership
- Consequences:
  ✅ Positives:
  - One version: API, workers, and web all run the exact same code
  - One source of truth: Business logic lives in one place (modules/*/impl/)
  - Shared contracts: Workers and API both depend on the same interface/ folders
  - Lane-aligned ownership: Clear who owns what
  - Operational simplicity: One build, one test suite, one security scan
  - Evolutionary path: Extract modules as services later only when needed
  - Compile-time safety: Build system enforces boundaries, illegal coupling = compile-time failure
  - Contract tests: Owned by QA-coder catch breaking changes early
  - Explicit dependencies: Each module declares deps in its own package.json
  
  ⚠️ Trade-offs:
  - Initial latency/throughput limits of single deployment (addressed via horizontal scaling within monolith)
  - Requires discipline to maintain boundaries (addressed via build system, tests, reviews)
  - Network calls between modules become in-process calls (performance benefit, but requires attention to failure modes)
- Constraints Imposed:
  1. Interface Sacredness: Treat module interfaces like API contracts—changing requires coordination
  2. Build System Enforcement: Compiler only allows impl/ → own interface/ + other interface/ + shared/
  3. Contract Tests: QA-coder owns tests verifying modules behave correctly per their interfaces
  4. Explicit Dependencies: Each module declares deps in its own package.json/pom.xml/etc.
  5. Worker Constraints: Workers depend only on module interface/—never on impl/ directly
  6. Lane Boundary Enforcement: 
     - backend-coder owns modules/*/impl/ (services, repos, workers) + workers/*/
     - api-coder owns public-api/ + reviews modules/*/interface/ changes
     - database-coder owns modules/*/impl/repositories/ + schema/migrations
     - qa-coder owns tests/contract-tests/, tests/api-tests/, worker/unit tests
     - security-specialist reviews auth/impl, data handling, secret usage
     - systems-architect owns overall boundaries, infra/, cross-cutting concerns
- Files / Modules Affected:
  - /src/modules/*/interface/ (PUBLIC CONTRACT)
  - /src/modules/*/impl/ (PRIVATE IMPLEMENTATION)
  - /src/modules/*/impl/services/ (Business logic)
  - /src/modules/*/impl/repositories/ (Data access)
  - /src/modules/*/impl/workers/ (Worker entrance points)
  - /src/public-api/ (EXTERNAL FACE)
  - /src/public-api/routes/ (API route definitions)
  - /src/workers/ (Alternative placement for worker entry points)
  - /infra/ (Deployment configurations)
  - /tests/ (Contract tests, API tests, etc.)
- Validation Method:
  1. Build System Checks: Illegal coupling results in compile-time failures
  2. Contract Test Suite: Owned by QA-coder, verifies modules behave correctly per interfaces
  3. Code Review Process: api-coder acts as gatekeeper for interface changes (reviews all modules/*/interface/ PRs)
  4. Dependency Audits: Each module's package.json shows explicit dependencies
  5. Lane Ownership Verification: Agents only modify files within their assigned lanes