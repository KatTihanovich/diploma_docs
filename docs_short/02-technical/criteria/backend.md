# Criterion: Backend

## Architecture Decision Record

### Status
**Status:** Accepted  
**Date:** 2026-01-06

### Context
Unity desktop game requires interaction with a database for player data (progress, achievements, game state). Challenges:

* Client must not access database directly (security)  
* Centralized business logic  
* Future extension support (mobile/web clients)  
* Unity requires standard communication mechanism  

### Decision
Implement a **Game API** as backend:

* Acts as intermediary between Unity client and database  
* Exposes HTTP endpoints consumed by Unity  
* Processes business logic and handles all database operations  
* Returns structured responses (JSON)  

Architecture:  
**Unity (Desktop Client) → Game API (Backend) → Database**  
Classic client–server separation ensures clear responsibilities.

### Alternatives Considered

| Alternative | Pros | Cons | Why Not Chosen |
|------------|------|------|----------------|
| Direct DB access from Unity | Simple, fewer components | Security risks, no access control, poor scalability | Unsafe for production |
| Ready-made backend solutions | Fast, prebuilt features | Limited flexibility, adaptation required, often paid | Custom API better fits requirements |
| Local storage only | Fast prototype, no server | No data sync, no persistence across devices | Does not meet project requirements |

---

### Consequences

**Positive:**  
- Isolated database improves security  
- Centralized logic and validation  
- Easier scalability and multi-client support  

**Negative:**  
- Increased system complexity  
- Extra maintenance effort  

**Neutral:**  
- Requires network for data operations (guest mode possible without saving)

---

## Implementation Details

### Key Implementation Decisions

| Decision | Rationale |
|----------|-----------|
| Java Spring Boot for backend | Simplifies REST API development, built-in DI, logging, security, industry standard |
| REST API over HTTPS | Secure, Unity-compatible client–server communication |
| Separation of client/server responsibilities | Unity handles game logic, backend handles persistence and business logic |
| Hibernate ORM for DB access | Abstracts SQL, improves maintainability, OOP access to data |

---

## Requirements Checklist

| # | Requirement | Status | Notes |
|---|-------------|--------|-------|
| 1 | Modern backend framework | ✅ | Java Spring Boot |
| 2 | Persistent data storage | ✅ | Relational database |
| 3 | ORM usage | ✅ | Hibernate |
| 4 | Multi-layered architecture | ✅ | Controllers, services, DAO |
| 5 | SOLID principles | ✅ | Clear separation, DI |
| 6 | API interaction | ✅ | REST endpoints documented (Swagger) |
| 7 | Global error handling | ✅ | Centralized exception mechanism |
| 8 | Logging | ✅ | Structured server-side logs |
| 9 | Production deployment | ✅ | Remote deployment |
|10 | Automated tests ≥70% coverage | ✅ | Unit & integration tests; CI/CD runs tests automatically |

---

## Known Limitations

| Limitation | Impact | Potential Solution |
|------------|--------|-------------------|
| Limited offline functionality | Guest mode does not save progress or achievements | Add local persistence with later synchronization |
