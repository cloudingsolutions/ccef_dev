# Architectural Decision Record

- ADR ID: ADR-CCEF-006
- Title: Deployment Architecture (Containerized with Orchestration)
- Status: Approved
- Product Slice IDs: PS-CCEF-001
- Related Requirement IDs: NFR-CCEF-013, NFR-CCEF-009
- Related Milestone IDs:
- Decision: Package the backend, frontend, and worker processes as Docker containers. Orchestrate containers using Kubernetes (or a managed Kubernetes service) for production deployments. Use Helm charts for repeatable releases. Maintain separate environments (dev, staging, prod) via namespaces or distinct clusters. Use infrastructure-as-code (e.g., Terraform) to provision clusters, networking, and managed services (databases, caches, KMS).
- Context: The system must be operable, observable, and scalable. Deployment should support rolling updates, secret management, and integration with cloud provider services (for credentials discovery). The architecture must be portable across environments.
- Options Considered:
  1. Traditional VM-based deployment (less agile, harder to scale).
  2. Serverless functions (e.g., AWS Lambda) for API and workers (challenges with long-running connections, state).
  3. Container orchestration with Kubernetes (chosen).
- Consequences:
  - Pros: Consistent environments, isolation, scaling per component, rich ecosystem for monitoring/logging, portable across cloud providers.
  - Cons: Operational overhead to manage cluster, learning curve, need for expertise in Kubernetes.
- Constraints Imposed:
  - Containers must run as non-root user where possible.
  - Sensitive data (encryption keys, credentials) injected via Kubernetes Secrets or CSI drivers, never baked into images.
  - Health checks (liveness/readiness) exposed per container to enable Kubernetes probing.
  - Resource limits (CPU/memory) defined per container to prevent noisy neighbors.
  - Logs sent to stdout/stderr for collection by cluster logging agent.
  - Use official base images (e.g., node:alpine, python:slim) and keep them patched.
  - Enable pod security policies or equivalent to restrict privileged containers.
- Files / Modules Affected:
  - Dockerfiles (backend, frontend, worker)
  - k8s/ (Kubernetes manifests: Deployments, Services, ConfigMaps, Secrets)
  - helm-charts/ (if using Helm)
  - terraform/ (infrastructure provisioning)
  - .github/workflows/ (CI/CD pipelines for building/pushing images and deploying)
- Validation Method:
  - Automated build and test of Docker images in CI.
  - Security scan of images for vulnerabilities.
  - End-to-end tests in a staging Kubernetes cluster.
  - Review of Helm charts for best practices.
  - Cost and performance monitoring in staging/prod.