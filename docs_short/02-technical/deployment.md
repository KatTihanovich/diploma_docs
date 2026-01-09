# Deployment & DevOps

## Infrastructure

### Deployment Architecture

```
┌─────────────────────────────────────────┐
│             Render Cloud                │
├─────────────────────────────────────────┤
│  ┌───────────────────────────────┐      │
│  │       Backend API Service      │      │
│  │   (Java Spring Boot, Docker)   │      │
│  │ - REST API                     │      │
│  │ - Auth & validation            │      │
│  │ - Game progress persistence    │      │
│  │ Port: 8080                     │      │
│  └───────────────────────────────┘      │
│             │                             │
│             ▼                             │
│  ┌───────────────────────────────┐      │
│  │      PostgreSQL Database       │      │
│  │ - Player profiles              │      │
│  │ - Progress & stats             │      │
│  │ Port: 5432                     │      │
│  └───────────────────────────────┘      │
└─────────────────────────────────────────┘
             ▲
             │ HTTPS (JSON)
┌─────────────────────────────────────────┐
│          Client Environment             │
├─────────────────────────────────────────┤
│  ┌───────────────────────────────┐      │
│  │       Unity Game Client        │      │
│  │      (Windows / macOS)        │      │
│  └───────────────────────────────┘      │
└─────────────────────────────────────────┘
```

### API Environments

| Environment | URL                                                                              | Branch |
| ----------- | -------------------------------------------------------------------------------- | ------ |
| Development | [http://localhost:8080](http://localhost:8080)                                   | dev    |
| Production  | [https://game-progress-api.onrender.com](https://game-progress-api.onrender.com) | main   |

## CI/CD Pipeline

### Overview

![Pipeline Schema](../assets/diagrams/CICD-pipeline-schema.png)

### Key Pipeline Steps

* **Build:** Maven clean package, upload artifact
* **Lint:** Checkstyle validation
* **Unit & Integration Tests:** Run tests, upload reports
* **Coverage & SonarCloud:** Verify code coverage, scan with SonarCloud
* **Deploy:** Trigger Render deployment, check health endpoint

> Branch rules: Only `main` triggers deploy; `dev` runs tests and checks only.

## Environment Variables

| Variable                    | Purpose           | Required | Example               |
| --------------------------- | ----------------- | -------- | --------------------- |
| DB_HOST                     | Database host     | Yes      | localhost             |
| POSTGRES_SUPERUSER          | DB superuser      | Yes      | postgres              |
| POSTGRES_SUPERUSER_PASSWORD | DB superuser pw   | Yes      | password              |
| POSTGRES_DB                 | Application DB    | Yes      | game_progress_db      |
| POSTGRES_USER               | App DB user       | Yes      | app_user              |
| GAME_APP_PASSWORD           | App DB pw         | Yes      | password              |
| BACKEND_PORT                | API port          | No       | 8080                  |
| JWT_SECRET                  | JWT signing key   | Yes      | your_jwt_secret       |
| JWT_EXPIRATION              | JWT expiration ms | No       | 86400000              |
| DB_MIGRATION_PATH           | Migration scripts | No       | path/to/db/migrations |
| DB_SEEDS_PATH               | Seed scripts      | No       | path/to/db/seeds      |
| ADMIN_PASSWORD              | Admin password    | Yes      | password              |

**Note:** Runtime vars are for deployed app; containerization vars for local Docker.
Secrets stored in `.env`, GitHub Secrets, and Render Environment Variables.

## Local Setup with Docker

### Prerequisites

* Docker & Docker Compose installed

### Steps

1. Clone repositories:

```bash
git clone https://github.com/KatTihanovich/game-progress-api
git clone https://github.com/KatTihanovich/game_progress_db
```

2. Create `.env` from `.env.example`
3. Navigate to docker-compose.yml folder:

```bash
cd path/to/api-repo/docker
```

4. Build and start containers:

```bash
docker-compose up --build
```

### Verify Installation

* Open [http://localhost:8080/actuator/health](http://localhost:8080/actuator/health) → should return `status: UP`
* Test API endpoints via Swagger: [http://localhost:8080/swagger-ui/index.html#/](http://localhost:8080/swagger-ui/index.html#/)
