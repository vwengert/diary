# Repository Instructions
## Goal
Build a diary application with:
- A backend web server
- A frontend web app
- Features to create and display diary entries
- Daily mood tracking
- Mood history view over time
## Product Requirements
- Users can create diary entries with at least:
  - date
  - title
  - content
- Users can list and view previous diary entries.
- Users can set or edit their mood for a specific day.
- The UI must display mood history (for example: chronological list or chart).
- Persist data so entries and moods remain available after restart.
## Suggested Architecture
- Keep backend and frontend as separate components in one repository.
- Backend exposes REST endpoints for entries and mood history.
- Frontend consumes backend API and renders:
  - entry creation form
  - entry list/detail views
  - mood editor
  - mood history view
## API Expectations
- `POST /api/entries` create an entry
- `GET /api/entries` list entries
- `GET /api/entries/{id}` get entry details
- `PUT /api/entries/{id}` update an entry
- `DELETE /api/entries/{id}` delete an entry
- `POST /api/mood` create mood for a date
- `PUT /api/mood/{date}` create/update mood for date
- `DELETE /api/mood/{date}` delete mood for date
- `GET /api/mood/history` return historical mood data
## Data Model Expectations
- Entry fields:
  - `id`
  - `date`
  - `title`
  - `content`
  - timestamps (`createdAt`, `updatedAt`)
- Mood fields:
  - `date`
  - `mood` (normalized set or numeric scale)
  - optional `note`
## Quality and Workflow
- Add input validation on backend and frontend.
- Add tests for API routes and critical UI behavior.
- Keep code modular and documented.
- Use consistent naming and folder structure.
## Devcontainer Path Requirement
When working in a devcontainer environment:
- Place and run project code from `/workspaces/diary`.
- Set devcontainer `workspaceFolder` to `/workspaces/diary`.
- Ensure all scripts, tooling, and documentation assume `/workspaces/diary` as the project root.

## Documentation Maintenance
- Keep `README.md` up to date with the current project scope, architecture, API expectations, and setup/workspace notes.
- Treat `documentation/` as the PlantUML source of truth for architecture and flows.
- For every feature, API, data model, or structural change, verify affected files in `documentation/` are still accurate and update them when needed.
- Do not finalize work while `README.md` or relevant PlantUML files are outdated.
