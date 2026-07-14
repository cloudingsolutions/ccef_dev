# Architectural Decision Record

- ADR ID: ADR-CCEF-004
- Title: Authentication and Authorization Mechanism
- Status: Approved
- Product Slice IDs: PS-CCEF-001
- Related Requirement IDs: FR-CCEF-001, FR-CCEF-002
- Related Milestone IDs:
- Decision: Use stateless JSON Web Tokens (JWT) for user authentication. Upon successful registration or sign-in, issue an access JWT (short-lived, e.g., 15 minutes) and a refresh JWT (longer-lived, e.g., 7 days) stored as HTTP-only, secure cookies. Protect routes with middleware that validates the access JWT and extracts user claims (user ID, roles, language preference). Implement role-based access control (RBAC) for future extensibility, though initial release only has basic registered-user role. For password handling, use strong hashing (bcrypt) with salt.
- Context: The system must allow users to register, sign in, and manage basic account settings. Requirements indicate that sign-in returns a JWT token and registration returns a session token. Localization and language preference must be persisted in the user profile.
- Options Considered:
  1. Stateful session tokens stored server-side (e.g., Redis).
  2. OAuth 2.0 for user authentication (overkill for first-party app).
  3. JWT-based stateless authentication (chosen).
- Consequences:
  - Pros: No server-side session storage, easy horizontal scaling, tokens contain necessary user info (language, ID).
  - Cons: Need to handle token revocation (use refresh token rotation and blacklist on logout), JWT size overhead, secure storage of refresh tokens.
- Constraints Imposed:
  - Access JWT short-lived (max 15 minutes) to limit exposure.
  - Refresh JWT stored as HTTP-only, secure, SameSite cookie to mitigate XSS/CSRF.
  - Passwords hashed using bcrypt with cost factor >= 12.
  - JWT signing key rotated periodically (e.g., every 30 days) with key ID (kid) header support.
  - HTTPS enforced in production; cookies set with Secure flag.
  - Language preference stored in user profile and reflected in JWT claims or retrieved via user service.
  - Authentication routes (login, registration) enforce rate limiting of max 5 attempts per minute per IP to prevent brute-force attacks.
- Files / Modules Affected:
  - src/backend/auth/ (JWT service, password hashing, middleware)
  - src/backend/models/user.ts (user entity)
  - src/backend/routes/auth.ts (registration, login, logout endpoints)
  - src/backend/middleware/auth.ts (JWT validation middleware)
  - src/backend/services/user-service.ts (user profile updates)
- Validation Method:
  - Automated tests for registration, login, token refresh, logout flows.
  - Security review of JWT implementation, cookie settings, password hashing.
  - Code review for proper middleware protection of routes.
  - Penetration testing for authentication bypass attempts.
  - Compliance verification that authentication mechanisms support GDPR (e.g., ability to delete user data).