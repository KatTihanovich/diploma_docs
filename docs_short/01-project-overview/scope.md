# Project Scope

## In Scope ✅

| Feature                      | Description                                                                                                              | Priority |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------ | -------- |
| Desktop Application on Unity | Cross-platform game build (Windows/macOS) with GUI; save/load progress via remote database; demo levels (story and boss) | Must     |
| Autonomous Game Agents       | Three enemies (FSM) and one boss (HFSM); Blackboard integration for behavior synchronization                             | Must     |
| Physics Simulation           | Vines and dynamic water reacting to player actions; interaction with floating objects                                    | Should   |
| Database & API Interaction   | Remote PostgreSQL database with necessary tables; Java REST API for Unity to read/write progress                         | Must     |
| CI/CD & Containerization     | GitHub Actions for automated build, test, deployment; Docker for local DB and API                                        | Should   |
| Automated Testing            | Unit and integration tests for Game API; basic coverage ≥70%                                                             | Must     |
| User Authentication          | UI for registration/login; API integration; JWT storage; field validation                                                | Must     |

## Out of Scope ❌

| Feature                                | Reason                                               |
| -------------------------------------- | ---------------------------------------------------- |
| Graphics, Animations, Character Models | Handled by artists and animators                     |
| Narrative, Storyline, Quests           | Handled by narrative team; demo focuses on mechanics |
| Network Play, Multiplayer              | Requires additional infrastructure; future phase     |
| In-Game Stores, Microtransactions      | Not part of academic scope; future phase             |
| Third-Party Game Engines               | Project uses Unity; others complicate integration    |
| Analytics, Telemetry, Marketing        | Outside technical scope; future phase                |
| Additional Levels Beyond Demos         | Diploma limited to two demo levels                   |

## Assumptions

* Stable access to remote server with API and DB
* Design assets and animations provided and integrated correctly
* Unity version supports cross-platform builds
* CI/CD environment has access to dependencies and network
* Docker installed for local development
* Unity Physics 2D handles collisions correctly
* Game API deployed and accessible
* Agents correctly subscribe/unsubscribe from Blackboard

## Constraints

* Time: limited by academic schedule; mitigated with planning and KPIs
* Budget: free tools only; use open-source solutions
* Technology: Unity (C#), PostgreSQL, Java Spring Boot; follow best practices
* Resources: single developer; modular architecture and team coordination
* Infrastructure: CI/CD limited by free tier; optimize pipelines
* Quality: API coverage ≥70%; critical endpoints tested; manual testing in Unity
* External: free hosting may have query limits; implement reconnection and monitoring

## Dependencies

| Dependency                             | Type      | Status |
| -------------------------------------- | --------- | ------ |
| Unity Engine 2023.x                    | Technical | ✅      |
| PostgreSQL 15.x                        | Technical | ✅      |
| GitHub Actions                         | External  | ✅      |
| Docker & Docker Compose                | Technical | ✅      |
| Java Spring Boot (Game API & REST API) | Technical | ✅      |
| Game API Hosting                       | External  | ⚠️     |
| Graphic & Audio Assets                 | Internal  | ⚠️     |
| Enemy Animations                       | Internal  | ⚠️     |
| UI/UX Elements                         | Internal  | ⚠️     |
| Free Hosting for PostgreSQL            | External  | ⚠️     |
