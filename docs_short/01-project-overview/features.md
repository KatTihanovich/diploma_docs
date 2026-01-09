# Features & Requirements

## Epics Overview

| Epic | Description                                                                              | Status |
| ---- | ---------------------------------------------------------------------------------------- | ------ |
| E1   | Game core development: basic game logic, agent architecture, environmental mechanics, UI | ✅      |
| E2   | Autonomous Agents: intelligent agents using FSM/HFSM and shared decision-making          | ✅      |
| E3   | Physics Simulation: ropes, vines, and dynamic water simulation                           | ✅      |
| E4   | Database Integration: remote PostgreSQL via API for storing user data                    | ✅      |
| E5   | CI/CD & Containerization: automated build, test, and deployment                          | ✅      |
| E6   | Automated Testing: unit and integration tests for code quality                           | ✅      |
| E7   | API Service: REST API for game-database interaction                                      | ✅      |

---

## User Stories

### Epic 1: Game Core Development

| ID       | User Story                                               | Acceptance Criteria                                                             | Priority | Status |
| -------- | -------------------------------------------------------- | ------------------------------------------------------------------------------- | -------- | ------ |
| US-E1-01 | Player controls character and interacts with environment | Character moves smoothly, collisions work, controls respond                     | Must     | ✅      |
| US-E1-02 | Player sees profile, progress, and game status           | UI displays profile, progress, status; updates in real time; remains responsive | Must     | ✅      |
| US-E1-03 | Player interacts with realistic rope/vine physics        | Ropes respond naturally and collisions behave correctly                         | Must     | ✅      |
| US-E1-04 | Developer integrates client-server communication         | Game state saved and retrieved via API; system handles failed requests          | Must     | ✅      |

### Epic 2: Autonomous Agents

| ID       | User Story                               | Acceptance Criteria                                                             | Priority | Status |
| -------- | ---------------------------------------- | ------------------------------------------------------------------------------- | -------- | ------ |
| US-E2-01 | Enemies exhibit state-based behavior     | Enemies switch between states correctly; detect player and attack appropriately | Must     | ✅      |
| US-E2-02 | Boss exhibits multi-phase behavior       | Boss transitions phases; minions respond; no logical conflicts                  | Must     | ✅      |
| US-E2-03 | Agents share info via centralized system | Blackboard accessible; parameters update; agents react correctly                | Must     | ✅      |

### Epic 3: Physics Simulation

| ID       | User Story                          | Acceptance Criteria                                                    | Priority | Status |
| -------- | ----------------------------------- | ---------------------------------------------------------------------- | -------- | ------ |
| US-E3-01 | Player interacts with dynamic vines | Vines return to position; simulation remains smooth                    | Should   | ✅      |
| US-E3-02 | Water reacts realistically          | Water responds to movements; objects float; simulation visually stable | Should   | ❌      |

### Epic 4: Database Integration

| ID       | User Story                                           | Acceptance Criteria                                                      | Priority | Status |
| -------- | ---------------------------------------------------- | ------------------------------------------------------------------------ | -------- | ------ |
| US-E4-01 | Stable connection between game and remote DB via API | API connection works; authentication succeeds; errors handled gracefully | Must     | ✅      |
| US-E4-02 | Auto-save and restore progress                       | Game saves automatically; works offline; syncs progress                  | Must     | ✅      |
| US-E4-03 | Account creation and login                           | Secure registration and login; progress tied to user identity            | Must     | ✅      |

### Epic 5: CI/CD & Containerization

| ID       | User Story                                    | Acceptance Criteria                                                 | Priority | Status |
| -------- | --------------------------------------------- | ------------------------------------------------------------------- | -------- | ------ |
| US-E5-01 | Automated build and tests on commits          | Pipeline triggers builds/tests automatically; deployment consistent | Should   | ✅      |
| US-E5-02 | Dockerized API and database for local testing | Containers start; DB accessible; Unity connects locally             | Should   | ✅      |

### Epic 6: Automated Testing

| ID       | User Story                          | Acceptance Criteria                                               | Priority | Status |
| -------- | ----------------------------------- | ----------------------------------------------------------------- | -------- | ------ |
| US-E6-01 | Cover critical API logic with tests | Test coverage ≥70%; all tests pass; failed tests block deployment | Must     | ✅      |

### Epic 7: API Service

| ID       | User Story                               | Acceptance Criteria                                                                                        | Priority | Status |
| -------- | ---------------------------------------- | ---------------------------------------------------------------------------------------------------------- | -------- | ------ |
| US-E7-01 | Secure API for game-database interaction | Endpoints respond correctly; authentication works; progress saved and retrieved; API documented and tested | Must     | ✅      |

---

## Use Case Diagram

![Usecase Diagram](../assets/diagrams/usecase-diagram.jpg)

---

## Non-Functional Requirements

### Performance

| Requirement        | Target                         |
| ------------------ | ------------------------------ |
| FPS                | ≥45                            |
| UI response        | Responsive during gameplay     |
| API response       | Fast under normal load         |
| Scene loading      | ≤5 seconds                     |
| Game save/load     | Fast and reliable              |
| Agent AI stability | No deadlocks or infinite loops |
| Cross-platform     | Windows and macOS              |

### Security

* JWT authentication with 24-hour expiration
* Secure access to user data and admin functions
* Data transmitted via HTTPS; passwords hashed
* Input sanitized and validated

### Accessibility

* Keyboard navigation
* Tooltips for new players

### Reliability

* Handles temporary server unavailability gracefully
* Supports offline mode with local saves
* Manual backups performed monthly

### Scalability

* Supports adding agents, levels, and mechanics without core changes

### Compatibility

| OS      | Minimum Version |
| ------- | --------------- |
| Windows | 10              |
| macOS   | 12              |
