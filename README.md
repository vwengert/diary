# Diary App
A full-stack diary project with a backend API and a frontend UI.
The application lets users create, view, update, and delete diary entries, manage daily mood values, and view mood history over time.

![Static Badge](https://img.shields.io/badge/Rust-1.86+-gold)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Build status](https://github.com/vwengert/diary/actions/workflows/test.yml/badge.svg?branch=main)](https://github.com/vwengert/diary/actions/workflows/test.yml)
[![codecov](https://codecov.io/github/vwengert/diary/graph/badge.svg?token=BQH6EBWNHS)](https://codecov.io/github/vwengert/diary)
![Repo Size](https://img.shields.io/github/repo-size/vwengert/diary)

## Core Features
- Diary entry CRUD (`create`, `read`, `update`, `delete`)
- Daily mood tracking and mood history
- Persistent storage via PostgreSQL

## Technology Stack
- **Language:** Rust (edition 2024)
- **Backend:** [Axum](https://github.com/tokio-rs/axum) 0.8, [Tokio](https://tokio.rs/) async runtime
- **Database:** PostgreSQL via [Diesel](https://diesel.rs/) 2.3 + [diesel-async](https://github.com/weiznich/diesel_async) with [bb8](https://github.com/djc/bb8) connection pool
- **Serialization:** serde / serde_json
- **Observability:** tracing

## Repository Structure
```
diary/                        # Workspace root
├── diary/                    # Shared library crate (domain types, helpers)
│   └── src/lib.rs
├── diary_backend/            # Backend web server crate (Axum REST API)
│   └── src/main.rs
├── documentation/            # PlantUML architecture diagrams
├── .github/
│   ├── copilot-instructions.md   # Repository coding & workflow instructions
│   └── workflows/                # CI pipelines (check, test, safety, scheduled)
├── Cargo.toml                # Workspace manifest
└── README.md
```

## API Endpoints
| Method   | Path                    | Description                     |
|----------|-------------------------|---------------------------------|
| `POST`   | `/api/entries`          | Create a new diary entry        |
| `GET`    | `/api/entries`          | List all diary entries          |
| `GET`    | `/api/entries/{id}`     | Get a single entry by ID        |
| `PUT`    | `/api/entries/{id}`     | Update an existing entry        |
| `DELETE` | `/api/entries/{id}`     | Delete an entry                 |
| `POST`   | `/api/mood`             | Create mood for a date          |
| `PUT`    | `/api/mood/{date}`      | Create or update mood for date  |
| `DELETE` | `/api/mood/{date}`      | Delete mood for a date          |
| `GET`    | `/api/mood/history`     | Return historical mood data     |

## Data Models
### Entry
| Field       | Type      | Description                      |
|-------------|-----------|----------------------------------|
| `id`        | UUID      | Unique identifier                |
| `date`      | Date      | Entry date                       |
| `title`     | String    | Entry title                      |
| `content`   | String    | Entry body text                  |
| `createdAt` | Timestamp | Creation timestamp               |
| `updatedAt` | Timestamp | Last update timestamp            |

### Mood
| Field  | Type          | Description                          |
|--------|---------------|--------------------------------------|
| `date` | Date          | The date this mood belongs to        |
| `mood` | Numeric/Enum  | Mood value (normalized scale or set) |
| `note` | String (opt.) | Optional note for the mood entry     |

## Architecture Documentation
### System Context
- [PlantUML C1 Main](documentation/C1-1-Main.puml)

### Container Context
_(to be added)_

### Component Context
_(to be added)_

## Local Development Setup
### Prerequisites
- Rust toolchain ≥ 1.86 ([rustup.rs](https://rustup.rs))
- PostgreSQL database instance
- `diesel_cli` for database migrations: `cargo install diesel_cli --no-default-features --features postgres`

### Build
```sh
cargo build
```

### Run Tests
```sh
cargo test
```

### Run Backend
```sh
# Set the DATABASE_URL environment variable first
set -x DATABASE_URL postgres://user:password@localhost/diary
cargo run -p diary_backend
```

## VS Code Devcontainer Setup

> **Note:** When working in a devcontainer, the project root is `/workspaces/diary`.
> All scripts, tooling, and documentation assume this path.

### Prerequisites
- Install Docker (or another OCI-compatible container runtime supported by the Dev Containers extension).
- Install Visual Studio Code.
- Install the VS Code extension `Dev Containers` (`ms-vscode-remote.remote-containers`).

### Open Project In Devcontainer
1. Open the project folder in VS Code.
2. Open the Command Palette (`Ctrl+Shift+P`).
3. Run `Dev Containers: Reopen in Container`.
4. Wait until the container build/start process is finished.
5. The workspace will be available at `/workspaces/diary`.
