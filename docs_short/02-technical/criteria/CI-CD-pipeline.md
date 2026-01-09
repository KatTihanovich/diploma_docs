# Criterion: CI/CD Pipeline

## Architecture Decision Record

### Status
**Status:** Accepted  
**Date:** 2026-01-06

### Context
The project is a Unity-based 2D platformer with a backend API for data storage and business logic. The backend API requires automated build, testing, and deployment to improve system stability, reduce manual errors, and accelerate release cycles.  
The Unity client is excluded from CI/CD due to platform-specific build dependencies and manual testing needs.

### Decision
Use **GitHub Actions** to implement CI/CD for the `game-progress-api` backend service.  
Pipeline stages include:

1. Build
2. Code style check (Checkstyle)
3. Unit testing
4. Integration testing
5. Code coverage analysis (JaCoCo + SonarCloud)
6. Deployment to Render

Pipeline triggers automatically on push and pull requests to `dev` and `master` branches. Deployment occurs **only on `master`** after all quality gates pass.

### Alternatives Considered

| Alternative         | Pros                                         | Cons                                        | Why Not Chosen                                  |
|--------------------|---------------------------------------------|--------------------------------------------|------------------------------------------------|
| Jenkins             | Full control, highly customizable          | Requires server, complex setup             | GitHub Actions integrates natively with repo  |
| GitLab CI/CD        | Integrated DevOps, container registry       | Migration, learning curve                  | Project already on GitHub                      |
| Manual deployment   | Direct control                               | Error-prone, time-consuming, no checks    | Automation required for stability             |

---

## Consequences

**Positive**
- Automated quality control: Checkstyle, JaCoCo, SonarCloud  
- Reduced deployment risk; only passing builds reach production  
- Faster release cycles with artifact generation  

**Negative**
- CI/CD limited to backend API; Unity client requires manual deployment  
- Depends on GitHub Actions and Render uptime  
- Initial setup time for workflow configuration  

**Neutral**
- Pipeline execution adds delay to merge process but ensures quality

---

## Implementation Details

### Project Structure

```
game-progress-api/
├── .github/
│   ├── workflows/
│   │   └── backend.yml
```

### Key Decisions

| Decision                        | Rationale                                                             |
|---------------------------------|---------------------------------------------------------------------|
| Sequential pipeline stages       | Ensures each quality gate passes before proceeding to next stage    |
| JaCoCo + SonarCloud integration | Provides objective code coverage and static analysis metrics        |
| Render Deploy Hook               | Automates deployment with health check verification                 |
| Artifact preservation            | Saves JAR and reports for post-build analysis and Docker image build|

---

## Requirements Checklist

| # | Requirement               | Status | Notes |
|---|---------------------------|--------|-------|
| 1 | Automated build           | ✅      | Maven compilation and JAR artifact |
| 2 | Code quality checks       | ✅      | Checkstyle + SonarCloud analysis |
| 3 | Automated testing         | ✅      | Unit & integration tests using H2 DB |
| 4 | Code coverage reporting   | ✅      | JaCoCo XML/HTML reports integrated with SonarCloud |
| 5 | Automated deployment      | ✅      | Render deployment with health checks on `master` branch |
| 6 | Artifact management       | ✅      | JAR, test reports, and coverage reports stored |
| 7 | Multi-environment support | ✅      | Dev (local), Test (CI), Production (Render) |

---

## CI/CD Stage Justification

- **Build:** Compile project and generate executable JAR (`./mvnw clean package -DskipTests`)  
- **Code Style Check (Lint):** Enforce Java coding standards via Checkstyle  
- **Unit Testing:** Validate individual components and business logic  
- **Integration Testing:** Test full API in Spring Boot context (H2 DB, MockMvc)  
- **Coverage & Quality Analysis:** JaCoCo + SonarCloud generate coverage, detect duplicates & vulnerabilities  
- **Deploy:** Trigger Render Deploy Hook after all stages pass; includes health check for service availability
