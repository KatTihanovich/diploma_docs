# 2. Technical Implementation

This section covers the technical architecture, design decisions, and implementation details.

## Contents

- [Tech Stack](tech-stack.md)
- [Criteria Documentation](criteria/) - ADR for each evaluation criterion
- [Deployment](deployment.md)

## Solution Architecture

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                         Honey & Bunny System                        │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│   ┌──────────────────┐        REST API        ┌──────────────────┐  │
│   │                  │ ────────────────────▶  │                  │ │
│   │   Unity Client   │                        │   Backend API    │  │
│   │  (Windows/macOS) │ ◀────────────────────  │ (Java Spring)    │  │
│   │                  │        JSON Response   │                  │  │
│   └──────────────────┘                        └──────────────────┘  │
│           │                                         │               │
│           │                                         ▼               │
│           │                              ┌─────────────────────┐    │
│           │                              │     PostgreSQL      │    │
│           │                              │   Remote Database   │    │
│           │                              └─────────────────────┘    │
│           │                                                         │
│           ▼                                                         │
│   ┌──────────────────────────┐                                      │
│   │   Local Game Systems     │                                      │
│   │                          │                                      │
│   │ - FSM / HFSM Agents      │                                      │
│   │ - Blackboard System      │                                      │
│   │ - Physics Simulation     │                                      │
│   │   (ropes, vines, water)  │                                      │
│   │ - UI & Game Logic        │                                      │
│   └──────────────────────────┘                                      │
│                                                                     │
│   ┌─────────────────────────────────────────────────────────────┐   │
│   │            CI / CD & Infrastructure                         │   │
│   │                                                             │   │
│   │  - GitHub Actions (build, tests)                            │   │
│   │  - Docker & Docker Compose                                  │   │
│   │  - Render (API + PostgreSQL, Free Tier)                     │   │
│   └─────────────────────────────────────────────────────────────┘   │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### System Components

| Component | Description | Technology |
|----------|-------------|------------|
| **Game Client** | Unity-based 2D platformer responsible for rendering, player input handling, physics simulation, and AI agent execution | Unity Engine 2023.x |
| **Backend API** | RESTful service handling persistent data storage, authentication, and communication between the game client and database | Java Spring Boot |
| **Database** | Stores player progress, game state data, and related entities | PostgreSQL 15 |
| **Hosting Platform** | Provides deployment and runtime environment for backend and database | Render (Free Tier) |
| **CI/CD Pipeline** | Automates build, test, and deployment processes for Game API | GitHub Actions |


### Data Flow

```
[User Action] → [Game] → [API Request] → [Backend(Game API)]
                                                 │
                                                 ▼
                                          [Business Logic]
                                                 │
                                                 ▼
                                          [Data Layer]
                                                 │
                                                 ▼
                                          [Database]
                                                 │
                                                 ▼
                                          [Response]
                                                 │
[UI Update] ← [Game] ← [API Response] ←─────┘
```

## Key Technical Decisions

| Decision | Rationale | Alternatives Considered |
|--------|-----------|------------------------|
| Use of FSM-based autonomous agents | FSM provides predictable, maintainable, and easily extensible enemy behavior suitable for 2D platformers | Behavior Trees, hardcoded scripts |
| Custom backend API implementation | Allows full control over data structures, avoids dependency on paid or opaque third-party solutions | Firebase, PlayFab |
| Client–server architecture | Separates game logic from data persistence, improves scalability and maintainability | Local-only data storage, direct connection between game client and database |
| PostgreSQL as DBMS | Reliable relational database suitable for structured game data | SQLite, NoSQL databases |

## Security Overview

| Aspect | Implementation |
|------|----------------|
| **Authentication** | Token-based authentication using JWT |
| **Authorization** | Endpoint-level access control using a shared access token for internal game communication |
| **Data Protection** | HTTPS for data in transit; database access restricted to backend service; passwords are hashed using bcrypt |
| **Input Validation** | Validation of incoming API requests using Spring Boot validation mechanisms |
| **Secrets Management** | Sensitive configuration values stored as environment variables locally in .evn and remotely in GitHub Secrets or Render environment variables |
