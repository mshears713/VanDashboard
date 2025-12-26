# Scripts Agent Guide: Automation & Maintenance

This folder contains the automation glue that turns the code into a running vehicle service.

## 1. Safety & Idempotency

- **"Do No Harm"**: Scripts must be idempotent (safe to run multiple times). Check for the existence of directories, users, or configs before creating them.
- **Dry Runs**: Where possible, provide a `--dry-run` flag for destructive operations (like system-wide configuration changes).

## 2. Key Categories

- **Bootstrap**: One-touch setup for a fresh Pi (installing Node, Python, camera drivers, etc.).
- **Service Management**: Scripts to install and configure `systemd` units for the Backend.
- **Networking**: Scripts to toggle between "Hotspot Mode" (vehicle use) and "Wi-Fi Client Mode" (home/update use).

## 3. Logging & Feedback

- **Exit Codes**: Always return proper exit codes (0 for success, non-zero for failure).
- **Agent Logs**: Capture script output to `~/vandashboard/logs/install.log` for debugging via the dashboard later.

---
*Reference: [docs/WORKFLOW.md](../docs/WORKFLOW.md) for deployment steps.*
