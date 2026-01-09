# Project Scope

## In Scope ✅


| Feature | Description | Priority |
|---------|-------------|---------|
| Desktop Application on Unity | Cross-platform game build for Windows and macOS; development of GUI for interacting with game features; correct saving and loading of user progress via remote database when wifi is turned on; creation of demo levels (story level and boss level) | Must |
| Autonomous Game Agents | Implementation of three enemies using FSM and one boss with HFSM; setup and integration of Blackboard for agent behavior synchronization and easy parameter adjustments | Must |
| Physics Simulation | Implementation of vines with correct physics and reaction to player actions; dynamic water simulation with interaction of floating objects | Should |
| Database & API Interaction | Creation of a remote PostgreSQL database with necessary tables (users, progress, game parameters); creation of a Java REST API service for Unity to interact with the database (read/write); correct operation with database via remote service under free hosting limitations | Must |
| CI/CD & Containerization | Setup of CI/CD pipeline (GitHub Actions) for automatic buil, testing, and deployment of Game API; containerization of local PostgreSQL database and Game API via Docker for testing and debugging | Should |
| Automated Testing | Development of unit and integration tests for Game API with basic logic coverage ≥70% | Must |
| User Authentication | Implementation of UI for registration and login; integration with API endpoints for authentication; local storage of JWT token for using authorization required endpoints; field validation (password ≥4 characters, unique username) | Must |


## Out of Scope ❌

| Feature | Reason | When Possible |
|---------|--------|---------------|
| Graphic Assets, Animations, Character Models | Implemented by other team members (artists, animators) | N/A - handled in parallel by the team |
| Narrative, Storyline, Quest Structure | Responsibility of narrative designers; demo project limited to mechanics demonstration | N/A - handled in parallel by the team |
| Network Play, Multiplayer Mode | Outside diploma requirements; requires additional infrastructure and time | Future phase |
| In-Game Stores, Microtransactions | Not part of academic requirements; commercial aspects not considered | Future phase |
| Third-Party Game Engines | Project built on Unity; using other engines (Unreal Engine) complicates integration | Never |
| Analytics, Telemetry, Marketing Reports | Outside technical requirements of the diploma | Future phase |
| Additional Levels Beyond Two Demos | Diploma project limited to two demo levels (story + boss) | Future phase |

## Assumptions

| # | Assumption | Impact if Wrong | Probability |
|---|------------|-----------------|-------------|
| 1 | Developer has stable access to remote server with API and PostgreSQL database | Unable to synchronize player data; need to switch to local storage | Low |
| 2 | Design, models, sprites, and animations are provided by other team members and correctly integrated | Integration delays; need to create placeholders; risk of version conflicts | Medium |
| 3 | Current Unity version supports cross-platform builds | Migration to another version may be required; loss of compatibility with some plugins | Low |
| 4 | CI/CD environment (GitHub Actions) has access to all dependencies and network resources | Automatic deployment fail; manual deploy and testing required | Medium |
| 5 | Docker is installed and functioning correctly for local development | Local DB and Game API testing impossible; dependence on remote DB and game API for development | Low |
| 6 | Unity Physics 2D correctly handles collisions and physics | Bugs in character and object physics; need custom physics implementation for objects that are using colliders | Low |
| 7 | Game API service is deployed and accessible via stable URL | Integration testing impossible; delays in client-server logic development | Medium |
| 8 | Agents correctly subscribe/unsubscribe from Blackboard | Memory leaks; unnecessary calculations; reduced performance | Medium |


## Constraints

Limitations that affect the project:

| Constraint Type | Description | Mitigation |
|-----------------|-------------|------------|
| Time | Deadlines are limited by academic calendar and diploma defense schedule | Careful planning with time buffers; weekly reports to supervisor; monitoring via KPIs and Git commits |
| Budget | Only free tools and software are used (Unity, PostgreSQL, Docker, GitHub, Render) | Use technologies with free tiers; utilize open-source solutions |
| Technology | Implementation in Unity using C#; database — PostgreSQL; Game API — Java Spring Boot | Study best practices for selected stack; follow official documentation |
| Resources | Development done by a single student; other aspects handled by team members | Modular architecture to isolate responsibilities; regular stand-ups with team |
| Infrastructure | CI/CD limited by free GitHub Actions tier (2000 min/month), limiting time and resources | Optimize pipeline to reduce build time (≤20 min per platform) |
| Quality | Basic API functionality coverage ≥70%; all critical endpoints respond correctly and handle errors gracefully; Manual testing in Unity | Prioritize unit and integration tests for all API endpoints; Code Review before merge |
| External | Working with remote DB and Game API via free hosting may have query limitations | Implement reconnection logic, timeouts, connection monitoring |

## Dependencies

| Dependency | Type | Owner | Status |
|------------|------|-------|--------|
| Unity Engine 2023.x | Technical | Unity Technologies | ✅ |
| PostgreSQL 15.x | Technical | PostgreSQL Global Development Group | ✅ |
| GitHub Actions | External | GitHub | ✅ |
| Docker & Docker Compose | Technical | Docker Inc. | ✅ |
| Java Spring Boot (Game API) | Technical | Internal Development | ✅ |
| Java Spring Boot (REST API) | Technical | Internal Development | ✅ |
| Game API Hosting | External | Free tier hosting on Render | ⚠️ |
| Graphic Assets (Sprites, Animations) | Internal | Artist Team | ⚠️ |
| Audio Assets (Music, SFX) | Internal | Sound Design Team | ⚠️ |
| Enemy Animations | Internal | Animation Team | ⚠️ |
| UI/UX Elements | Internal | Design Team | ⚠️ |
| Free Hosting for PostgreSQL | External | Free tier hosting on Render(1GB limit, 30-day expiration) | ⚠️ |
