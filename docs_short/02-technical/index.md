# 2. Technical Implementation

This section outlines the technical architecture, design decisions, and implementation.

## Contents

* [Tech Stack](tech-stack.md)
* [Criteria Documentation](criteria/) - ADRs for evaluation criteria
* [Deployment](deployment.md)

## Solution Architecture

### High-Level Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                         Honey & Bunny System                        │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│   ┌──────────────────┐        REST API        ┌──────────────────┐  │
│   │   Unity Client   │ ────────────────────▶  │   Backend API    │  │
│   │  (Windows/macOS) │ ◀────────────────────  │ (Java Spring)    │  │
│   └──────────────────┘        JSON Response   └──────────────────┘  │
│           │                                         │               │
│           ▼                                         ▼               │
│   ┌──────────────────────────┐                 ┌──────────────┐    │
│   │   Local Game Systems     │                 │ PostgreSQL   │    │
│   │ - FSM / HFSM Agents      │                 │ Remote DB    │    │
│   │ - Blackboard System      │                 └──────────────┘    │
│   │ - Physics (ropes, vines)│                                      │
│   │ - UI & Game Logic        │                                      │
│   └──────────────────────────┘                                      │
│                                                                     │
│   ┌─────────────────────────────────────────────────────────────┐   │
│   │            CI / CD & Infrastructure                         │   │
│   │ - GitHub Actions (build/tests)                               │   │
│   │ - Docker & Docker Compose                                     │   │
│   │ - Render (API + PostgreSQL, Free Tier)                        │   │
│   └─────────────────────────────────────────────────────────────┘   │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

### System Components

| Component            | Description                                                                       | Technology         |
| -------------------- | --------------------------------------------------------------------------------- | ------------------ |
| **Game Client**      | Unity-based 2D platformer handling rendering, input, physics, AI                  | Unity 2023.x       |
| **Backend API**      | REST service for data storage, authentication, and communication with game client | Java Spring Boot   |
| **Database**         | Stores player progress, game state, and related entities                          | PostgreSQL 15      |
| **Hosting Platform** | Deployment and runtime for backend & DB                                           | Render (Free Tier) |
| **CI/CD Pipeline**   | Automates build, test, and deployment of Game API                                 | GitHub Actions     |

### Data Flow

```
[User Action] → [Game] → [API Request] → [Backend]
                                          │
                                          ▼
                                     [Business Logic]
                                          │
                                          ▼
                                      [Database]
                                          │
                                          ▼
                                      [Response]
                                          │
[UI Update] ← [Game] ← [API Response] ←───┘
```

## Key Technical Decisions

| Decision                   | Rationale                                  | Alternatives                             |
| -------------------------- | ------------------------------------------ | ---------------------------------------- |
| HFSM and FSM-based agents  | Predictable, maintainable AI               | Behavior Trees, hardcoded scripts        |
| Custom backend API         | Full control, avoids paid/opaque solutions | Firebase, PlayFab                        |
| Client–server architecture | Separates logic & data, scalable           | Local-only storage, direct DB connection |
| PostgreSQL                 | Reliable relational DB                     | SQLite, NoSQL                            |

## Security Overview

| Aspect                 | Implementation                                            |
| ---------------------- | --------------------------------------------------------- |
| **Authentication**     | JWT token-based                                           |
| **Authorization**      | Endpoint-level access via shared token                    |
| **Data Protection**    | HTTPS, DB access restricted, bcrypt-hashed passwords      |
| **Input Validation**   | Spring Boot request validation                            |
| **Secrets Management** | Env variables locally (.env) and remotely (GitHub/Render) |
