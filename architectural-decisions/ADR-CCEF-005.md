# Architectural Decision Record

- ADR ID: ADR-CCEF-005
- Title: API Design (RESTful JSON API)
- Status: Approved
- Product Slice IDs: PS-CCEF-001
- Related Requirement IDs: FR-CCEF-004, FR-CCEF-010, FR-CCEF-011, FR-CCEF-012 (and others that imply API interactions)
- Related Milestone IDs:
- Decision: Implement a RESTful JSON API with versioned endpoints (e.g., /api/v1/). Use standard HTTP methods (GET, POST, PUT, PATCH, DELETE) for resource operations. Return JSON payloads for successful responses and use application/problem+json for error responses per RFC 7807. Use plural nouns for resource names (e.g., /forecasts, /providers, /budgets). Implement pagination using limit/offset or cursor-based where appropriate. Use ISO 8601 strings for timestamps in JSON. Support content negotiation for JSON only in initial release.
- Context: The system provides a responsive web application that interacts with a backend server for user management, provider connections, forecasting, budgeting, alerts, etc. The API must be usable by the frontend and potentially by third-party integrations in the future.
- Options Considered:
  1. GraphQL API (flexible but added complexity).
  2. REST-like but with custom action endpoints (less standardized).
  3. Strict RESTful JSON API (chosen).
- Consequences:
  - Pros: Widely understood, easy to cache, good tooling (Swagger/OpenAPI), clear contract.
  - Cons: May require multiple endpoints for related data; over-fetching/under-fetching possible.
- Constraints Imposed:
  - API versioned under /api/v1/ (increment major version for breaking changes).
  - All API responses JSON unless otherwise documented; errors follow RFC 7807.
  - Timestamps in ISO 8601 format (UTC).
  - Use plural resource names and nest sub-resources logically (e.g., /providers/{id}/credentials).
  - Implement idempotency for POST/PUT/PATCH where appropriate (e.g., via Idempotency-Key header).
  - Secure all endpoints with JWT authentication (see ADR-CCEF-004).
  - Enable CORS only for trusted origins (the frontend domain).
- Files / Modules Affected:
  - src/backend/routes/ (API route definitions)
  - src/backend/controllers/ (request handlers)
  - src/backend/services/ (business logic)
  - src/backend/middleware/ (validation, authentication, error handling)
  - src/backend/utils/api-response.ts (helper functions)
  - docs/api/ (OpenAPI specification)
- Validation Method:
  - Automated contract tests (e.g., using Pact or OpenAPI validation).
  - Manual QA verifies API behavior matches specification.
  - Code review ensures adherence to REST principles and error handling.
  - API review with frontend team to ensure usability.
  - Compliance check that API does not leak sensitive data in error messages.