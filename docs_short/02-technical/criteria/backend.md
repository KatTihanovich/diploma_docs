# Criterion: Backend

## Architecture Decision Record

### Status

**Status:** Accepted

**Date:** 2026-01-06

### Context

The project is a **desktop game developed using Unity**, which needs to interact with a **database** to store and retrieve player-related data such as progress, game state, achievements, and other persistent information.

The main problem to address is the need for **secure, reliable, and scalable communication between the desktop client and the database**.

Key forces and constraints:

* The client application must not have direct access to the database for security reasons.
* Game rules and business logic should be centralized and controlled in one place.
* The architecture should allow future extension (e.g., adding a mobile or web client).
* Unity as a desktop client requires a standard and well-supported communication mechanism.

### Decision

The chosen solution is to implement a **Game API** that acts as the **backend** and an intermediary layer between:

* the Unity desktop client, and
* the database.

The Game API:

* exposes HTTP endpoints consumed by the Unity client;
* processes requests according to the game’s business logic;
* performs all database read/write operations;
* returns structured responses (e.g., JSON) back to the client.

The resulting architecture is:

**Unity (Desktop Client) → Game API (Backend) → Database**

This decision follows a classic **client–server architecture**, ensuring clear separation of responsibilities between layers.

### Alternatives Considered

| Alternative                          | Pros                                    | Cons                                                    | Why Not Chosen                                                 |
| ------------------------------------ | --------------------------------------- | ------------------------------------------------------- | -------------------------------------------------------------- |
| Direct database access from Unity    | Simple implementation, fewer components | Severe security risks, no access control, hard to scale | Exposing the database to the client is unsafe and unacceptable |
| Using ready-made backend solutions | Fast setup, out-of-the-box functionality          | Limited flexibility, requires adaptation, often paid               | Custom Game API better matches project-specific requirements           |
| No backend (local data storage only) | Fast prototyping, no server needed      | No data synchronization, no persistence across devices  | Does not meet project requirements                             |

### Consequences

**Positive:**

* Improved security by isolating the database from the client
* Centralized business logic and validation
* Easier scalability and support for multiple clients

**Negative:**

* Increased system complexity
* Additional effort required to maintain the backend

**Neutral:**
* Network connectivity is required for data-related operations or guest mode can be used(it does not save data)

## Implementation Details

### Key Implementation Decisions

| Decision | Rationale |
|----------|-----------|
| Use Java with Spring Boot for backend development | Spring Boot is a modern server-side framework that simplifies REST API development, provides built-in dependency injection, logging, and security, and aligns with industry best practices |
| REST API communication over HTTPS | REST over HTTPS is a standard, secure, and Unity-compatible approach for reliable client–server communication |
| Separation of client-side and server-side responsibilities | Game logic is handled by the Unity desktop client, while the backend manages data persistence, validation, and business logic |
| Database interaction via Hibernate ORM | Hibernate abstracts direct SQL usage, improves maintainability, and enables object-oriented data access |

## Requirements Checklist

| # | Requirement | Status | Evidence / Notes |
|---|-------------|--------|------------------|
| 1 | Use of a modern backend framework | ✅ | Backend implemented using Java Spring Boot |
| 2 | Persistent data storage | ✅ | Relational database used for storing game and player state |
| 3 | Use of ORM | ✅ | Hibernate ORM used for database access |
| 4 | Multi-layered architecture | ✅ | Controllers, services, and data access layers implemented |
| 5 | SOLID design principles | ✅ | Clear separation of responsibilities and dependency injection |
| 6 | API interaction description | ✅ | REST endpoints documented (Swagger) |
| 7 | Global error handling | ✅ | Centralized exception handling mechanism |
| 8 | Logging | ✅ | Structured server-side logging implemented |
| 9 | Production deployment | ✅ | Application deployed in a remote production environment |
|10 | Automated test coverage (≥ 70%) | ✅ | Unit and integration tests implemented; coverage is more than 70%; there is CI/CD pipeline to run tests automatically |

## Known Limitations

| Limitation | Impact | Potential Solution |
|------------|--------|-------------------|
| Limited offline functionality | In offline mode, gameplay is available but progress, achievements, and results are not saved | Implement local persistence with synchronization when connection is restored |
