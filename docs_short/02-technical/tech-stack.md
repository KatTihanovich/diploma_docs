# Technology Stack

## Stack Overview

| Layer          | Technology              | Version      | Justification |
|----------------|-----------------------|-------------|---------------|
| **Desktop(Client)**     | Unity (C#)            | 6000.0.51      | Chosen as the main platform for 2D game development, cross-platform for Windows/macOS, supports physics, FSM/HFSM, and Blackboard AI |
| **Backend**    | Java Spring Boot       | 3.4.1        | Provides a robust, scalable framework for REST API development, integrates well with PostgreSQL and Docker, supports unit/integration testing |
| **Database**   | PostgreSQL             | 15        | Managed relational database for persistent game data, supports SQL queries, reliable and free-tier available on Render |
| **Containerization** | Docker & Docker Compose| -           | Containerization simplifies deployment, ensures environment consistency, and supports CI/CD pipelines |
| **CI/CD**      | GitHub Actions         | -           | Automates build, test, and deployment of backend API, ensures stable releases and reproducible environment |
| **Testing**    | JUnit / Spring Test    | -           | Supports automated unit and integration tests of API, ensures ≥70% code coverage |
| **Deployment**      |Render                    | —           | Render (Free Tier) is selected for hosting the backend API and database, providing remote access and integration with CI/CD at no additional cost.|

## Key Technology Decisions

### Decision 1: FSM-Based Autonomous Agents

**Context:**  
Enemies needed to behave autonomously, logically, and consistently within the 2D platformer environment.

**Decision:**  
Implement **FSM/HFSM with Blackboard** inside Unity.

**Rationale:**
- Provides predictable and repeatable AI behavior.  
- Easy to extend and maintain for future gameplay features.  
- Integrates smoothly with physics and other game systems.

**Trade-offs:**
- **Pros:** Modularity, reusability, stable foundation for future expansion.  
- **Cons:** Requires careful state planning; debugging complexity increases with many agents.  

---

### Decision 2: Custom Backend API Implementation

**Context:**  
The game required a backend system for storing player progress and other game data, while avoiding dependency on third-party solutions.

**Decision:**  
Develop a **custom Game API** using **Java Spring Boot**.

**Rationale:**
- Full control over data structures and API design.  
- Avoids costs or limitations of paid/opaque third-party services.  
- Supports unit and integration testing for reliability.

**Trade-offs:**
- **Pros:** Stability, scalability, easier maintenance and expansion.  
- **Cons:** Heavier than lightweight backend alternatives; requires Java knowledge.  

---

### Decision 3: Client–Server Architecture

**Context:**  
Game logic and data persistence needed to be separated to ensure maintainability and scalability.

**Decision:**  
Adopt a **client–server architecture** connecting Unity client with the backend Game API.

**Rationale:**
- Improves modularity of game logic and data handling.  
- Simplifies integration of new gameplay features.  
- Allows remote database access for persistent progress and analytics.

**Trade-offs:**
- **Pros:** Scalability, maintainability, separation of concerns.  
- **Cons:** Slightly higher complexity than local-only solutions; requires network handling.  

---

### Decision 4: PostgreSQL as Database

**Context:**  
The game needed a reliable storage solution for structured game data like player progress, scores, and settings.

**Decision:**  
Use a **managed PostgreSQL database** (Render Free Tier).

**Rationale:**
- Reliable relational database suitable for structured data.  
- Integrates well with Java Spring Boot backend.  
- Provides free remote hosting for development and testing.

**Trade-offs:**
- **Pros:** Reliability, structured queries, remote access for team.  
- **Cons:** Free-tier limitations (1 GB, sleep mode, no built-in backups).


## Development Tools

| Tool               | Purpose                                       | Notes |
|-------------------|-----------------------------------------------|-------|
| **IDE**           | IntelliJ IDEA / Visual Studio Code            | Used for backend(Game API) development (Spring Boot) and C# scripts for Unity; includes extensions for Java, Docker, Git |
| **Unity** | Game development (2D platformer, AI, UI)   | Version 6000.0.51; used for implementing gameplay mechanics, FSM/HFSM agents, physics simulations, and Unity UI Toolkit |
| **Version Control** | Git                                          | Branching strategy: dev for development and testing, main for production |
| **Package Manager** | Maven                                         | Manages Java dependencies for Spring Boot project |
| **Linting**       | Checkstyle                                     | Ensures code quality, follows Java coding standards |
| **Testing**       | JUnit / Spring Test                           | Unit and integration tests for API, target ≥70% coverage |
| **API Testing**   | Postman                                       | Manual testing of REST API endpoints, checking response and status codes |
| **Documentation** | Swagger                                       | API documentation and endpoint description, used for integration with Unity client |
| **Containerization** | Docker / Docker Compose          | Ensures consistent environment|

## External Services & APIs

| Service | Purpose | Pricing Model |
|---------|---------|---------------|
| Render | Used to host database and Game API remotely | Free tier|
