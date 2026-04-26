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
- Persistent storage for entries and moods

## Architecture Documentation
### System Context
- [PlantUML C1 Main](documentation/C1-1-Main.puml)

### Container Context

### Component Context

## Repository Structure
- `src` - main application source code
- `.github/copilot-instructions.md` - repository coding and workflow instructions
- `documentation` - PlantUML documentation that should stay aligned with implementation

## VS Code Devcontainer Setup
### Prerequisites
- Install Docker (or another OCI-compatible container runtime supported by the Dev Containers extension).
- Install Visual Studio Code.
- Install the VS Code extension `Dev Containers` (`ms-vscode-remote.remote-containers`).

### Open Project In Devcontainer
1. Open the project folder in VS Code.
2. Open the Command Palette (`Ctrl+Shift+P`).
3. Run `Dev Containers: Reopen in Container`.
4. Wait until the container build/start process is finished.
