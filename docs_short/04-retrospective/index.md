# Project Retrospective

## Successes ✅

**Technical:**

* Clear separation between Unity client and backend API
* Stable API integration for progress, achievements, and levels
* Backend API design is Unity-friendly
* Automated testing and CI/CD improved backend confidence
* DTOs reduced integration issues

**Process:**

* Minimal rework connecting Unity to API
* Parallel development of client and API possible
* Quick validation of backend changes

**Personal:**

* Gained experience with Unity, C#, and Java API
* Learned client-server integration and API design

## Challenges ⚠️

| Planned                  | Outcome                | Cause                                | Impact |
| ------------------------ | ---------------------- | ------------------------------------ | ------ |
| Water simulation         | Not implemented        | Too CPU/GPU heavy; purely decorative | Medium |
| CI/CD for Unity          | Only backend automated | Unity builds require manual testing  | Low    |
| Automated tests for game | Only backend tested    | Unity relies on manual testing       | Low    |

**Other Challenges:**

* First-time FSM usage increased development time; resolved by simplifying FSM design
* Remote DB limited lifetime required migrations and reinitialization scripts

## Technical Debt & Known Issues

| ID     | Issue                              | Severity | Fix                                                   |
| ------ | ---------------------------------- | -------- | ----------------------------------------------------- |
| TD-001 | Offline progress not saved         | Medium   | Local storage and deferred sync with backend          |
| TD-002 | Unity client lacks automated tests | Medium   | Introduce Unity Test Framework for key gameplay logic |
| TD-003 | Manual FSM config for enemies      | Low      | Use node/graph configuration                          |

**Code Quality Issues:**

* Unity code lacks comments and tests; legacy code quality varies

## Future Improvements

**High Priority:**

* Offline authentication (cache credentials)
* Offline progress sync

**Medium Priority:**

* CI/CD for Unity builds

**Nice to Have:**

* Decorative water interactions and physics-based environmental puzzles

## Lessons Learned

**Technical:**

* FSM/HFSM scales better than monolithic AI scripts
* Simplified or decorative physics often sufficient
* Client-server separation simplifies development

**Process:**

* Early scope validation avoids unnecessary work
* Manual testing more effective for complex gameplay

**Different Approach Next Time:**

* Plan architecture and resource requests earlier
* Focus on meaningful gameplay simulations instead of complex decorative features

## Personal Growth

| Skill          | Before   | After        |
| -------------- | -------- | ------------ |
| FSM/HFSM       | Beginner | Intermediate |
| Rope physics   | Beginner | Intermediate |
| Unity client   | Beginner | Intermediate |
| CI/CD & Docker | Beginner | Intermediate |

**Key Takeaways:**

1. Early architecture decisions affect scalability
2. Only implement features adding real gameplay value
3. Clear system separation simplifies development and testing

*Retrospective completed: 2026-01-09*
