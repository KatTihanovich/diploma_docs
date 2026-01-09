# Criterion: CI/CD Pipeline

## Architecture Decision Record

### Status

**Status:** Accepted 

**Date:** 2026-01-06

### Context

The diploma project consists of a Unity-based platformer game with a backend API for data storage and business logic. The backend API component requires automated build, testing, and deployment processes to reduce delivery time, improve system stability, and minimize manual deployment errors. The Unity client application was excluded from CI/CD automation due to platform-specific build dependencies and manual testing requirements.
​
### Decision

Implement a comprehensive CI/CD pipeline using GitHub Actions for the game-progress-api backend service with automated stages including build, code style checking, unit testing, integration testing, code coverage analysis, and deployment to Render cloud platform. The pipeline triggers automatically on push and pull requests to master and dev branches, with deployment occurring only on master branch after all quality gates pass.
​
### Alternatives Considered

| Alternative         | Pros                                                    | Cons                                                                                       | Why Not Chosen                                                                             |
| ------------------- | ------------------------------------------------------- | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------ |
| Jenkins | Full control over infrastructure, highly customizable   | Requires dedicated server maintenance, additional infrastructure costs, more complex setup | GitHub Actions provides native integration with repository without infrastructure overhead |
| GitLab CI/CD        | Integrated DevOps platform, built-in container registry | Requires migration from GitHub, additional learning curve for team                         | Project already hosted on GitHub with established workflows                                |
| Manual deployment   | No automation setup required, direct control            | High error rate, time-consuming, no automated quality checks, inconsistent deployments     | Automation essential for maintaining code quality and reducing deployment risks            |

## Consequences

### Positive
- Automated quality control through integrated Checkstyle, JaCoCo, and SonarCloud analysis
- Reduced deployment risk by ensuring all tests pass before production release
- Faster release cycles with automated build and deployment processes
- Consistent environment configuration between testing and production
- Comprehensive test coverage metrics and artifact generation for reporting

### Negative
- CI/CD pipeline limited to backend API only, Unity client requires manual deployment
- Dependency on GitHub Actions availability and Render platform uptime
- Initial setup time for configuring workflows and quality gates

### Neutral
- Pipeline execution time adds delay to merge process but ensures quality

## Implementation Details

### Project Structure

```
game-progress-api/
├── .github/
│   ├── workflows/
│   │   └── backend.yml
```

### Key Implementation Decisions

| Decision                        | Rationale                                                                                                                             |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- |
| Sequential pipeline stages      | Ensures each quality gate passes before proceeding, preventing deployment of broken builds    |
| JaCoCo + SonarCloud integration | Generates objective code coverage metrics required for project reporting and quality standards  |
| Render Deploy Hook              | Automates deployment with health check verification to ensure service availability          |
| Artifact preservation           | Enables post-build analysis and provides executable JAR for Docker image creation         |

## Requirements Checklist

| # | Requirement               | Status | Evidence/Notes                                                                                          |
| - | ------------------------- | ------ | ------------------------------------------------------------------------------------------------------- |
| 1 | Automated build process   | ✅      | Maven compilation with JAR artifact generation            |
| 2 | Code quality checks       | ✅      | Checkstyle for style, SonarCloud for static analysis           |
| 3 | Automated testing         | ✅      | Unit and integration test stages with H2 database             |
| 4 | Code coverage reporting   | ✅      | JaCoCo generates XML/HTML reports, integrated with SonarCloud     |
| 5 | Automated deployment      | ✅      | Render deployment with health checks on master branch      |
| 6 | Artifact management       | ✅      | JAR, test reports, and coverage reports stored in GitHub Actions |
| 7 | Multi-environment support | ✅      | Dev (local), Test (CI), Production (Render) environments        |

## Justification of CI/CD Stages

- **Build**: Compile the project and generate executable JAR (`./mvnw clean package -DskipTests`). Ensures correct compilation and provides artifact for testing and deployment.  

- **Code Style Check (Lint)**: Use Checkstyle (`./mvnw checkstyle:check`) to enforce Java coding standards, ensuring consistency and easier maintenance.  

- **Unit Testing**: Verify individual components and business logic in isolation. Provides quick feedback and reduces regression risks.  

- **Integration Testing**: Test components together in a real Spring Boot context using H2, Spring Security Test, and MockMvc. Ensures correct API, JPA, and security integration.  

- **Code Coverage & Quality Analysis**: Generate JaCoCo reports and run SonarCloud analysis for duplicates, vulnerabilities, and coverage metrics. Artifacts saved for reporting.  

- **Deploy**: Deploy via Render Deploy Hook after all tests pass. Automation reduces deployment risks, ensures consistency, and speeds up release.
