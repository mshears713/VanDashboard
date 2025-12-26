# VanDashboard

A Raspberry-Pi-based vehicle dashboard system displayed on an Android phone via local Wi-Fi.

## Project Structure

- `backend/`: Server and APIs (Python/Node.js).
- `frontend/`: TypeScript-based web UI.
- `docs/`: Architecture diagrams and technical notes.
- `scripts/`: Helper scripts for deployment and development.
- `config/`: Configuration templates for the Pi and services.

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
