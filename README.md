# VanDashboard

A Raspberry-Pi-based vehicle dashboard system displayed on an Android phone via local Wi-Fi.

## Project Structure

This project is organized into modular directories, each containing its own **`AGENTS.md`** for detailed technical guidance.

- `backend/`: Server logic & hardware orchestration. ([README](backend/README.md) | [AGENTS](backend/AGENTS.md))
- `frontend/`: High-visibility TS/Web UI. ([README](frontend/README.md) | [AGENTS](frontend/AGENTS.md))
- `docs/`: Master blueprints, architecture, and workflows. ([AGENTS](docs/AGENTS.md))
- `scripts/`: Deployment & maintenance automation. ([AGENTS](scripts/AGENTS.md))
- `config/`: Infrastructure & environment templates. ([AGENTS](config/AGENTS.md))

### Documentation Quick Links
- [Architecture Overview](docs/ARCHITECTURE.md)
- [Development Workflow](docs/WORKFLOW.md)
- [Runtime Model](docs/RUNTIME_MODEL.md)
- [Operating Modes](docs/MODES.md)

## Local Development (WSL/Windows)

1. **Frontend**:
   ```bash
   cd frontend
   npm install
   npm run dev
   ```
2. **Backend**:
   ```bash
   cd backend
   # Setup instructions will depend on chosen language
   ```

## Pi Deployment

The system is designed to run headless on a Raspberry Pi, serving the frontend `dist/` folder via the backend server.

---
*For more details, see [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md)*
