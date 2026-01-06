# Problem Statement & Goals

## Context

Honey & Bunny is a story-oriented 2D platformer that combines elements of adventure and psychological drama. The game explores the inner world of the individual, transforming emotions into the force necessary to overcome challenges. The main character, Bunny, journeys through a symbolic path of self-discovery, where every emotion becomes a tool for development. Players explore internal locations of consciousness, solve logical puzzles, and interact with manifestations of fears and feelings to achieve inner harmony and save their inner child, Honey.

The team project aims to create a complete interactive product that integrates artistic, psychological, and technical components. 

**The purpose of the diploma project** is to develop, implement, and integrate the key technical systems that support the game’s functionality. This includes FSM-based autonomous agents, physics simulations for environmental objects, and a backend database infrastructure for storing player progress. These systems form the technical foundation of the game, enabling other team members to continue developing story content, levels, animations, and audiovisual elements.

Currently, the project exists as a playable demo version that can be downloaded and run on computers. Core gameplay mechanics have been implemented, including autonomous agent behavior, environmental physics interactions, and persistent data storage. Ongoing development focuses on expanding the game content, such as additional story chapters, level design, animations, sound effects, and visual polish. While there are existing 2D platformers exploring psychological or emotional themes, Honey & Bunny distinguishes itself by integrating emotional states directly into gameplay mechanics, making emotions a tangible tool for progression.

From a technical perspective, the development of custom components was necessary to provide a clear, maintainable, and scalable architecture. By creating the autonomous agents, physics systems, backend API, and database, the project mostly avoids dependency on external or paid solutions, simplifies integration of new gameplay mechanics, and establishes a robust foundation for future expansion and maintenance.

## Problem Statement

**Who:** Game developers working on Honey & Bunny and end users (players) interacting with the Unity-based game.  

**What:** Developers face challenges integrating game mechanics, enemies behaviors, and backend services using existing third-party solutions, which may be costly, inflexible, or insufficiently documented. Players require stable gameplay, consistent enemy AI behavior, and the ability to save progress.  

**Why:** Without maintainable and scalable core systems, the development team cannot efficiently expand the game or implement new features, and players experience unstable gameplay, lost progress, and inconsistent interactions. Developing in-house technical components ensures smooth development, high-quality user experience, and more independence from external or paid solutions.


### Pain Points

| # | Pain Point | Severity | Current Workaround |
|---|-----------|----------|--------------------|
| 1 | Lack of centralized storage for player progress across multiple devices | High | Use of local files, which prevents data synchronization and limits scalability |
| 2 | Unstable behaviour of enemies and game objects without autonomous agents (FSM/HFSM), leading to bugs and degraded gameplay | High | Monolithic code, without modularity and without the possibility of simple code reuse  |
| 3 | Risk of errors during deploy of game API and testing due to lack of automation (CI/CD), which does not align with modern DevOps practices and complicates project maintenance | Medium | Manual build and testing processes, increasing development time and error risk |
| 4 | System vulnerability caused by direct Unity-to-database connection: risk of unauthorized access, SQL injections, or user-side data manipulation | High | Absence of a backend API for operation control, error handling, and data consistency |

## Business Goals

| Goal | Description | Success Indicator |
|-----|------------|-------------------|
| Development of a stable cross-platform application | Ensuring correct operation on Windows and macOS; organizing user progress storage and interaction with a remote PostgreSQL database via an API | Correct operation on both platforms without critical errors; API response time ≤800 ms if it is up |
| Creation of autonomous game agents with diverse behaviour | Implementation of three enemies based on FSM and one boss using HFSM; use of a shared data storage (Blackboard) to synchronize agent behaviour | ≥90% correct FSM/HFSM transitions; FPS ≥45 with 4 active enemies |
| Implementation of physical object simulations | Simulation of vines and dynamic water surface reacting to player movement; correct interaction with floating objects | Correct vine and water behaviour in ≥85% of test scenarios |
| Ensuring reliable development, testing, and maintenance of the backend | Configuration of a CI/CD pipeline for automated build, testing, and API deployment; use of Docker for local database and API deployment; test coverage ≥70% | ≥95% successful CI/CD builds; test coverage ≥70%; Docker container startup time ≤5 minutes |


## Objectives & Metrics

| Objective | Metric | Current Value | Target Value | Timeline |
|----------|--------|---------------|--------------|----------|
| Functional implementation completeness | Percentage of implemented functional requirements (agents, object physics, database integration) | 90% | 90% | According to thesis defense schedule |
| Test coverage | Percentage of API code covered by automated tests | 88% | 80% (minimum requirement: 70%) | According to thesis defense schedule |
| Build stability | Percentage of successful builds in the CI/CD pipeline | 90% | 90% | Continuous monitoring |
| Agent performance | FPS with all 4 agents running simultaneously on demo levels | - | ≥45 FPS | After development completion |
| API response time | Average response time for requests to a remote database via API | ≤800 ms | ≤800 ms | After development completion |


## Success Criteria

### Must Have

- [ ] Functional completeness: Implementation of 90% of functional requirements (agents, object physics, database integration)
- [ ] Test coverage: ≥70% of code of API covered by automated tests
- [ ] Build stability: ≥90% successful builds in CI/CD pipeline (GitHub Actions)
- [ ] Cross-platform compatibility: Correct operation on Windows and macOS without critical errors
- [ ] Agent performance: FPS ≥45 with 4 agents running simultaneously on demo levels
- [ ] Correct component integration: Successful operation of all modules without critical errors
- [ ] Data saving/loading system response time: Average API response time ≤800 ms after initial launch
- [ ] Correct agent behaviour: ≥90% correct FSM/HFSM transitions
- [ ] Accuracy of physical simulations: Correct rope and liquid simulation behaviour in ≥85% of test scenarios

### Nice to Have

- [ ] 80% test coverage: Exceeding the minimum test coverage threshold for APIs
- [ ] 60 FPS performance: Achieving target performance with all agents running
- [ ] Build stability 95%: Achieving maximum CI/CD stability
- [ ] Content integration 100%: Full compatibility of all visual and audio resources with technical components

## Non-Goals

What this project explicitly does NOT aim to achieve:

- Development of graphic assets, animations, and character models (implemented by other team members)

- Creation of narrative, storyline, and quest structure (limited demonstration of mechanics)

- Implementation of online gameplay, multiplayer mode, in-game shops, and microtransactions
​
- Implementation of custom game engine
​
- Analytics, telemetry, and marketing reports
​
- Development of additional levels beyond the two demo levels (story level and boss battle level)
