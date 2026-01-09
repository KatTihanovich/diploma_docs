# Technology Stack

## Stack Overview

| Layer          | Technology              | Version      | Justification |
|----------------|------------------------|-------------|---------------|
| **Desktop(Client)** | Unity (C#)            | 6000.0.51  | 2D game, cross-platform (Windows/macOS), supports FSM/HFSM, Blackboard AI |
| **Backend**    | Java Spring Boot       | 3.4.1       | Scalable REST API, integrates with PostgreSQL & Docker, supports testing |
| **Database**   | PostgreSQL             | 15          | Reliable relational DB, free remote hosting on Render, structured game data |
| **Containerization** | Docker & Docker Compose | -        | Simplifies deployment, ensures environment consistency, supports CI/CD |
| **CI/CD**      | GitHub Actions         | -           | Automates build, test, deployment for backend API |
| **Testing**    | JUnit / Spring Test    | -           | Automated unit/integration tests, ≥70% coverage |
| **Deployment** | Render                 | —           | Free hosting for backend API and database |

---

## Key Technology Decisions

### 1. FSM-Based Autonomous Agents
- **Context:** Enemies require consistent autonomous behavior.
- **Decision:** FSM/HFSM with Blackboard in Unity.
- **Rationale:** Predictable, maintainable, easily extensible; integrates with physics.
- **Trade-offs:** Modular but requires careful state planning.

### 2. Custom Backend API
- **Context:** Store player progress without relying on third-party services.
- **Decision:** Java Spring Boot Game API.
- **Rationale:** Full control over data, avoids paid limitations, supports testing.
- **Trade-offs:** Heavier than alternatives; requires Java knowledge.

### 3. Client–Server Architecture
- **Context:** Separate game logic and data persistence.
- **Decision:** Unity client + backend API.
- **Rationale:** Modularity, easier feature integration, persistent remote progress.
- **Trade-offs:** Slightly higher complexity, requires network handling.

### 4. PostgreSQL as Database
- **Context:** Store structured game data.
- **Decision:** Managed PostgreSQL (Render Free Tier).
- **Rationale:** Reliable, integrates with Spring Boot, remote access for team.
- **Trade-offs:** Free-tier limits (1GB, sleep mode, no backups).

---

## Development Tools

| Tool               | Purpose                                       |
|-------------------|-----------------------------------------------|
| **IDE**           | IntelliJ IDEA / VS Code for Java & Unity C# |
| **Unity**         | 2D game, AI, physics, UI                     |
| **Version Control** | Git (dev/main branching strategy)           |
| **Package Manager** | Maven for Java dependencies                  |
| **Linting**       | Checkstyle for code quality                  |
| **Testing**       | JUnit / Spring Test (≥70% coverage)         |
| **API Testing**   | Postman                                      |
| **Documentation** | Swagger                                      |
| **Containerization** | Docker / Docker Compose                     |

---

## External Services & APIs

| Service | Purpose | Pricing Model |
|---------|---------|---------------|
| Render  | Host DB and Game API remotely | Free tier |
