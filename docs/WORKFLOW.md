# Development & Deployment Workflow

This document outlines the daily workflow for developing in WSL and deploying to the Raspberry Pi.

## 1. Daily Development Workflow (WSL)

Always work in **WSL** on your laptop for the best compatibility with the Pi's Linux environment.

1.  **Pull Latest**: Start by ensuring your local repo is up to date.
    ```bash
    git pull origin main
    ```
2.  **Edit & Test**: Make changes and run the local development servers.
    - **Frontend**: `npm run dev` (inside `frontend/`)
    - **Backend**: Run your server script (e.g., `python main.py` or `node index.js`)
3.  **Local Validation**: Open `localhost:<port>` in your browser to verify changes.
4.  **Commit & Push**:
    ```bash
    git add .
    git commit -m "Brief description of changes"
    git push origin main
    ```

---

## 2. Deployment Workflow (Raspberry Pi)

Deployment is handled via Git handoff. Access your Pi via SSH.

1.  **SSH into Pi**:
    ```bash
    ssh pi@<pi-ip-address>
    ```
2.  **Pull Changes**: Navigate to the project root and pull.
    ```bash
    cd ~/VanDashboard
    git pull origin main
    ```
3.  **Update Dependencies**: Only required if `package.json` or `requirements.txt` changed.
    - **Frontend**: `npm install && npm run build` (if building on Pi)
    - **Backend**: `pip install -r requirements.txt` or `npm install`
4.  **Restart Server**:
    - **Manual**: Kill the old process and run the new one.
    - **Service (Future)**: `sudo systemctl restart vandashboard.service`
5.  **Verify**: Access the Pi's IP from your Android phone browser.

---

## 3. Definition of Done Checklist

- [ ] Code is formatted and linted.
- [ ] Backend serves the latest Frontend `dist/` build.
- [ ] Dashboard is accessible at `http://<pi-ip>`.
- [ ] No critical errors in the server logs.

---

## 4. Common Failure Cases & Fast Debugging

| Failure | Likely Cause | Fast Fix |
| :--- | :--- | :--- |
| **"Connection Refused"** | Server isn't running or port is wrong. | Check `ps aux` or `netstat -tulpn` on Pi. |
| **"Old UI showing"** | Frontend wasn't rebuilt or browser cache. | Run `npm run build`; hard refresh phone browser. |
| **"Module Not Found"** | Missing dependency on Pi. | Re-run the install command for backend/frontend. |

---
*Note: As we scale, we will move to `systemd` for auto-restarting services.*
