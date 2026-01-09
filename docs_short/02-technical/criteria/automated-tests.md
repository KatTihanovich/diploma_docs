# Criterion: Automated Tests Coverage

## Architecture Decision Record

### Status
**Status:** Accepted  
**Date:** 2026-01-05

### Context
The backend API stores player progress and game data. Automated tests are required to prevent regressions, ensure reliable behavior, and maintain consistency of game state. A minimum of **70% code coverage** ensures confidence in critical functionality and safe future development.

### Decision
Implement automated **unit and integration tests** using **JUnit**, **Spring Boot Test**, and **H2 in-memory database**. Critical endpoints, data persistence, and error handling are covered. CI via **GitHub Actions** runs tests on each commit to `dev` or `main`, generating coverage metrics to maintain ≥70% coverage.

### Alternatives Considered

| Alternative | Pros | Cons | Why Not Chosen |
|-------------|------|------|----------------|
| No automated tests | No extra effort | High regression risk | Fails coverage requirement |
| Unit tests only | Fast, easy | Miss integration and persistence errors | Does not cover full API workflows |
| Manual testing | Simple bug detection | Time-consuming, inconsistent, non-repeatable | Cannot provide coverage metrics or automated regression detection |

---

## Consequences

**Positive**
- Ensures API works as intended, reduces regressions  
- Provides measurable ≥70% coverage for maintainability  
- Facilitates safe feature development

**Negative**
- Initial test implementation adds development time  
- Ongoing maintenance required as API evolves  

**Neutral**
- Coverage alone does not catch all edge-case bugs; some manual testing remains useful

---

## Implementation Details

### Project Structure

```
game-aprogress-api/src/test
```

### Key Decisions

| Decision | Rationale |
|----------|-----------|
| Use JUnit, Spring Boot Test, H2, JaCoCo | Robust unit & integration tests; supports CI/CD and coverage reports |
| CI/CD via GitHub Actions | Automatically executes tests on each commit/PR to maintain code quality |
| ≥70% coverage target | Ensures measurable reliability and maintainable, well-tested code |

---

## Requirements Checklist

| # | Requirement                         | Status | Notes |
| - | ----------------------------------- | ------ | ----- |
| 1 | Unit tests for API endpoints        | ✅      | Critical endpoints covered with JUnit, CI executed |
| 2 | Integration tests for Game API      | ✅      | Database interactions, API responses, error handling tested |
| 3 | ≥70% code coverage                  | ✅      | Verified with CI-generated reports |
| 4 | Automatic CI execution              | ✅      | Tests run on each commit and PR via GitHub Actions |

---

## Known Limitations

| Limitation                          | Impact | Potential Solution |
| ----------------------------------- | ------ | ---------------- |
| No Unity client tests               | Only backend tested | Use Unity Test Framework for client tests in future |
| Test maintenance required           | Must update tests with API changes | Integrate test updates into development workflow |
