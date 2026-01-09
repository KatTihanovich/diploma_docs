# Criterion: Automated tests covarage

## Architecture Decision Record

### Status

**Status:** Accepted

**Date:** 2026-01-05

### Context

The backend API responsible for storing player progress and game data requires reliable and maintainable behavior. Without automated tests, changes to the API could introduce regressions, break endpoints, or cause inconsistent game state, negatively impacting both developers and players. A minimum of 70% code coverage by automated tests is required to provide confidence that critical functionality works as intended and to support safe future development and integration of new features.

### Decision

To satisfy the requirement of ≥70% code coverage, the backend API was developed with automated unit and integration tests using JUnit, Spring Boot Test and H2-in-memory database. Critical API endpoints, data persistence logic, and error handling routines were covered by these tests. Continuous integration via GitHub Actions ensures that tests are executed automatically on each commit to dev or main, preventing regressions and maintaining code quality. Test results and coverage metrics are monitored to verify that the 70% threshold is consistently met.

### Alternatives Considered

| Alternative | Pros | Cons | Why Not Chosen |
|-------------|------|------|----------------|
| No automated tests | No additional development effort | High risk of regressions; errors could go undetected | Would not satisfy the requirement for ≥70% coverage and maintainable code |
| Only unit tests | Tests individual functions quickly; easy to implement | Does not cover API integration or persistence; might miss errors in real workflows | Does not cover integration between components or the full request/response flow; might miss errors in how different parts of the API interact, which is critical for maintaining player progress and data integrity |
| Manual testing | Can catch simple bugs using Postman for testing | Very time-consuming, inconsistent, and non-repeatable; cannot measure coverage | Cannot provide consistent coverage metrics and does not automate regression detection |

### Consequences

**Positive:**
- Ensures that critical API functionality works as intended and reduces the risk of regressions.
- Provides measurable code coverage (≥70%) to demonstrate reliability and maintainability.
- Facilitates safe future development and easier integration of new features.

**Negative:**
- Initial setup and writing of automated tests requires additional development time.
- Continuous maintenance of tests is necessary as the API evolves.
- Tests must be updated whenever the API code changes, which adds ongoing maintenance effort.

**Neutral:**
- Test coverage alone does not guarantee that all possible bugs are caught; manual testing may still be required for edge cases.


## Implementation Details

### Project Structure

```
game-aprogress-api/src/test
```

### Key Implementation Decisions

| Decision | Rationale |
|----------|-----------|
| Use of JUnit, Spring Boot Test, H2, and JaCoCo for automated testing | Provides robust unit and integration testing for API endpoints; integrates with CI/CD; supports coverage reporting and analysis. |
| CI/CD via GitHub Actions | Ensures tests run automatically on each commit and pull request, preventing regressions and maintaining code quality. |
| ≥70% coverage target | Ensures a measurable reliability standard for the API and demonstrates maintainable, well-tested code. |

## Requirements Checklist

| # | Requirement                         | Status | Evidence/Notes                                                             |
| - | ----------------------------------- | ------ | -------------------------------------------------------------------------- |
| 1 | Unit tests for API endpoints        | ✅      | Covered critical endpoints with JUnit; executed via GitHub Actions CI.     |
| 2 | Integration tests for Game API      | ✅      | Tests cover database interactions, REST API responses, and error handling. |
| 3 | ≥70% code coverage                  | ✅      | Verified with coverage reports generated during CI runs.                   |
| 4 | Automatic execution in CI           | ✅      | GitHub Actions pipeline triggers on each commit and PR.                    |

## Known Limitations

| Limitation                          | Impact                                                            | Potential Solution                                                                             |
| ----------------------------------- | ----------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| No Unity client tests               | Only API is covered; client-side logic not automatically verified | Implement unit or integration tests for Unity using Unity Test Framework in future iterations. |
| Test maintenance required           | Whenever API changes, tests must also be updated                  | Establish clear test update workflow alongside code changes to keep coverage consistent.       |


