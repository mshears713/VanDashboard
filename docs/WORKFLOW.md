# Development & Deployment Workflow

This document outlines the daily workflow for developing in WSL and deploying to the Raspberry Pi.

## 1. Daily Development Workflow (WSL)

1.  **Pull Latest**: `git pull origin main`
2.  **Edit & Test**: 
    - Frontend: `cd frontend && npm run dev`
    - Backend: `cd backend && <run-server-cmd>`
3.  **Local Validation**: Check `localhost` to verify logic.
4.  **Commit & Push**: `git add . && git commit -m "..." && git push`

## 2. Deployment Workflow (Raspberry Pi)

1.  **SSH into Pi**: `ssh pi@<pi-ip>`
2.  **Pull Changes**: `cd ~/VanDashboard && git pull origin main`
3.  **Build/Update**:
    - Frontend: `npm run build` (if building on Pi)
    - Backend: `pip install -r requirements.txt` or `npm install`
4.  **Restart Server**: `sudo systemctl restart vandashboard.service` (once configured).

## 3. Definition of Done

- [ ] Features tested in WSL.
- [ ] Frontend `dist/` is correctly served by Backend.
- [ ] No regressions in hardware connectivity logs.

---
*Reference: [AGENTS.md](AGENTS.md) for detailed folder rules.*
