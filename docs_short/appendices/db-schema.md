# Database Schema

## Overview

| Attribute | Value |
|-----------|-------|
| **Database** | PostgreSQL |
| **Version** | 15 |
| **ORM** | Hibernate |

## Entity Relationship Diagram

![Database Diagram](../assets/diagrams/database-diagram.png)

## Tables

### Table 1: users

Stores player account records.

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| user_id | BIGSERIAL | PK | Primary key |
| nickname | VARCHAR(255) | NOT NULL, UNIQUE, CHECK (LENGTH(TRIM(nickname)) > 0) | Player’s nickname (username) |
| password_hash | TEXT | NOT NULL | Hash of player’s password |
| age | INTEGER | CHECK (age > 0 AND age < 100) | Player’s age |
| created_at | TIMESTAMP | NOT NULL, DEFAULT CURRENT_TIMESTAMP | Record creation date |
| updated_at | TIMESTAMP | NOT NULL, DEFAULT CURRENT_TIMESTAMP | Last update date |

**Indexes:**
- `idx_users_nickname` (Unique)  
- `idx_users_created_at`  

---

### Table 2: levels

Reference list of game levels.

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| level_id | BIGSERIAL | PK | Primary key |
| level_name | TEXT | NOT NULL, UNIQUE, CHECK (LENGTH(TRIM(level_name)) > 0) | Level name |
| boss_on_level | BOOLEAN | NOT NULL, DEFAULT FALSE | Indicates whether the level has a boss |
| stars_on_level | INTEGER | NOT NULL, DEFAULT 0 | Number of stars that are on level |
| created_at | TIMESTAMP | NOT NULL, DEFAULT CURRENT_TIMESTAMP | Record creation date |
| updated_at | TIMESTAMP | NOT NULL, DEFAULT CURRENT_TIMESTAMP | Last update date |

**Indexes:**
- `idx_levels_name` (Unique)  

---

### Table 3: progress

Stores player progress on each level.

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| progress_id | BIGSERIAL | PK | Primary key |
| user_id | BIGINT | FK → users.user_id, NOT NULL | Player reference |
| level_id | BIGINT | FK → levels.level_id, NOT NULL | Level reference |
| killed_enemies_number | INTEGER | NOT NULL, DEFAULT 0, CHECK (killed_enemies_number >= 0) | Number of killed enemies on this level |
| solved_puzzles_number | INTEGER | NOT NULL, DEFAULT 0, CHECK (solved_puzzles_number >= 0) | Number of solved puzzles on this level |
| time_spent | VARCHAR(8) | NOT NULL, DEFAULT '00:00:00', CHECK (time_spent ~ '^[0-9]{2}:[0-9]{2}:[0-9]{2}$') | Time spent on level |
| stars | INTEGER | NOT NULL, DEFAULT 0, CHECK (stars >= 0) | Number of collected stars |
| created_at | TIMESTAMP | NOT NULL, DEFAULT CURRENT_TIMESTAMP | Record creation date |

**Indexes:**
- `idx_progress_user_level` on (user_id, level_id)  

---

### Table 4: achievements

Stores possible achievements.

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| achievement_id | BIGSERIAL | PK | Primary key |
| achievement_name | TEXT | NOT NULL, UNIQUE, CHECK (LENGTH(TRIM(achievement_name)) > 0) | Achievement name |
| achievement_description | TEXT | NULLABLE | Description of how to obtain the achievement |
| created_at | TIMESTAMP | NOT NULL, DEFAULT CURRENT_TIMESTAMP | Record creation date |
| updated_at | TIMESTAMP | NOT NULL, DEFAULT CURRENT_TIMESTAMP | Last update date |

**Indexes:**
- `idx_achievements_name` (Unique)  

---

### Table 5: users_achievements

Implements many-to-many relationship between users and achievements.

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| user_achievement_id | BIGSERIAL | PK | Primary key |
| user_id | BIGINT | FK → users.user_id, NOT NULL | Player reference |
| achievement_id | BIGINT | FK → achievements.achievement_id, NOT NULL | Achievement reference |
| created_at | TIMESTAMP | NOT NULL, DEFAULT CURRENT_TIMESTAMP | Record creation date |

**Constraints:**
- UNIQUE (`user_id`, `achievement_id`)  

**Indexes:**
- `idx_users_achievements_user_achievement` on (user_id, achievement_id)  

---

### Table 6: users_statistics

Stores player’s full pre-computed statistics.

| Column | Type | Constraints | Description |
|--------|------|-------------|-------------|
| statistics_id | BIGSERIAL | PK | Primary key |
| user_id | BIGINT | FK → users.user_id, NOT NULL, UNIQUE | Player reference |
| total_levels_completed | INTEGER | NOT NULL, DEFAULT 0, CHECK (total_levels_completed >= 0) | Number of unique levels completed |
| total_time_played | VARCHAR(8) | NOT NULL, DEFAULT '00:00:00', CHECK (total_time_played ~ '^[0-9]{2}:[0-9]{2}:[0-9]{2}$') | Total time played on all levels |
| total_killed_enemies | INTEGER | NOT NULL, DEFAULT 0, CHECK (total_killed_enemies >= 0) | Total enemies killed |
| total_solved_puzzles | INTEGER | NOT NULL, DEFAULT 0, CHECK (total_solved_puzzles >= 0) | Total puzzles solved |
| total_stars | INTEGER | NOT NULL, DEFAULT 0, CHECK (total_stars >= 0) | Total stars collected |
| created_at | TIMESTAMP | NOT NULL, DEFAULT CURRENT_TIMESTAMP | Record creation date |
| updated_at | TIMESTAMP | NOT NULL, DEFAULT CURRENT_TIMESTAMP | Last update date |

**Indexes:**
- `idx_users_statistics_user_id` on user_id  

---

## Relationships

| Relationship | Type | Description |
|--------------|------|-------------|
| users → progress | One-to-Many | Each user can have multiple progress records |
| levels → progress | One-to-Many | Each level can have multiple progress records |
| users → users_achievements | One-to-Many | Each user can have multiple achievements |
| achievements → users_achievements | One-to-Many | Each achievement can belong to multiple users |
| users → users_statistics | One-to-One | Each user has exactly one statistics record |


## Migrations

| Version | Description                                                                 | Date            | Status |
|--------:|-----------------------------------------------------------------------------|-----------------|--------|
| V1 | Create role for database user | Initial setup | ✅ |
| V2 | Create table `users` with fields: `user_id`, `nickname`, `password_hash`, `age`, `timestamps` | Initial setup | ✅ |
| V3 | Create table `levels` with fields: `level_id`, `level_name`, `boss_on_level`, `timestamps` | Initial setup | ✅ |
| V4 | Create table `progress` with fields: `progress_id`, `user_id`, `level_id`, `killed_enemies_number`, `solved_puzzles_number`, `time_spent`, `timestamps` | Initial setup | ✅ |
| V5 | Create table `achievements` with fields: `achievement_id`, `achievement_name`, `achievement_description`, `timestamps` | Initial setup | ✅ |
| V6 | Create table `users_achievements` (junction table) with fields: `user_achievement_id`, `user_id`, `achievement_id`, `timestamps` | Initial setup | ✅ |
| V7 | Create table `users_statistics` with fields: `statistics_id`, `user_id`, `total_levels_completed`, `total_time_played`, `total_killed_enemies`, `total_solved_puzzles`, `timestamps` | Initial setup | ✅ |
| V8 | Create triggers for automatic update of `updated_at` field on all tables | Initial setup | ✅ |
| V9 | Insert reference data for `levels` and `achievements` | Initial setup | ✅ |
| V10 | Insert test data for `users` and `progress` (seed data) | Development / Testing | ✅ |
