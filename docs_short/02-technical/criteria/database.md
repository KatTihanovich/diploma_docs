# Criterion: Database

## Architecture Decision Record

### Status
**Status:** Accepted  
**Date:** 2026-01-06

### Context
The 2D platformer requires a relational database to store player accounts, level progress, achievements, and statistics.  
Requirements:

- Support multiple concurrent players  
- Maintain data integrity and transactional consistency  
- Fast queries for statistics and leaderboards  
- Access only via backend API, no direct client access  

### Decision
Use **PostgreSQL**:

**Schema:**  
- Six core tables: `users`, `levels`, `achievements`, `progress`, `users_achievements`, `users_statistics`  
- Pre-computed `users_statistics` for fast queries  
- Indexed for performance  

**Data Access:**  
- Operations via Spring Boot API  
- Single application role (`game_app`) with controlled privileges  
- Versioned schema via Flyway  
- Automatic timestamps via triggers  

**Architecture:**  
**Unity Client → Game API → PostgreSQL**

---

### Alternatives Considered

| Alternative | Pros | Cons | Why Not Chosen |
|-------------|------|------|----------------|
| NoSQL (MongoDB) | Flexible, scalable | Weak ACID, inefficient relational queries | ACID and relational integrity required |
| SQLite | Lightweight, serverless | Local-only, no multi-user access | Remote DB needed for centralized progress |
| MySQL | Mature, widely adopted | Weaker constraints, limited JSON | PostgreSQL provides better integrity & extensibility |

---

### Consequences

**Positive:**  
- Strong integrity via foreign keys, triggers, constraints  
- ACID transactions prevent data corruption  
- Fast leaderboard queries via pre-computed stats  
- Version-controlled schema via Flyway  
- Secure API-based access  

**Negative:**  
- Time stored as `VARCHAR(8)` requires parsing  
- Pre-computed stats need synchronization logic  
- More setup required vs embedded DB  

**Neutral:**  
- Single application role simplifies security but requires API-level authorization  
- Schema may need refactoring as game features expand  

---

## Implementation Details

### Project Structure

```
game_progress_db/
├── db/
│   ├── scripts/
│   │   └── create_database.sql          # Initial database creation
│   ├── migration/                        # Flyway version-controlled migrations
│   │   ├── V1__create_role.sql          # Application role setup
│   │   ├── V2__create_users_table.sql
│   │   ├── V3__create_levels_table.sql
│   │   ├── V4__create_progress_table.sql
│   │   ├── V5__create_achievements_table.sql
│   │   ├── V6__create_users_achievements_table.sql
│   │   ├── V7__create_users_statistics_table.sql
│   │   ├── V8__create_triggers_update_updated_at.sql
│   │   └── V9__insert_reference_data.sql
│   └── seeds/                           # Test data scripts
|       ├── V10__test_data.sql
```

### Key Implementation Decisions

| Decision | Rationale |
|----------|-----------|
| Bigserial IDs as PKs | Stable auto-increment IDs |
| Separate `users_statistics` table | Pre-computed aggregates for fast queries |
| Composite indexes on FKs | Optimizes common queries |
| `VARCHAR` time + regex | Human-readable, HH:MM:SS enforced via CHECK |
| Cascade deletion | Maintains referential integrity |
| Unique constraints | Prevent duplicates |
| `updated_at` triggers | Automatic timestamp updates |

### Diagram

![Database Diagram](../../assets/diagrams/database-diagram.png)

---

## Requirements Checklist

| # | Requirement | Status | Notes |
|---|-------------|--------|-------|
| 1 | Relational DB with normalized schema | ✅ | Six tables in 3NF |
| 2 | Data integrity via constraints | ✅ | PKs, FKs, UNIQUE, CHECK, NOT NULL enforced |
| 3 | Indexing for performance | ✅ | Composite indexes + unique keys |
| 4 | ACID transactions | ✅ | Rollback on violation |
| 5 | User authentication storage | ✅ | Password hashes only |
| 6 | Schema version control | ✅ | Flyway migrations |
| 7 | Automated timestamps | ✅ | Triggers update `updated_at` |
| 8 | Role-based access control | ✅ | `game_app` role with controlled privileges |

---

## Known Limitations

| Limitation | Impact | Potential Solution |
|------------|--------|------------------|
| Single role lacks granular permissions | All API operations share same privileges | Create multiple roles mapped to API endpoints |
| No soft delete | Deleted users permanently lose data | Add `is_deleted` flag and filtered indexes |
| Time format max 99:59:59 | Cannot track >99 hours of play | Use `INTERVAL` type if needed |

---

## References
[Database migrations repository](https://github.com/KatTihanovich/game_progress_db)
