# Runtime Model: The Van as a Personal Utility

This document defines the operational behavior of the VanDashboard system. It functions as a "personal appliance"—stable and automatic, but transparent and resilient for the owner-builder.

## 1. The Personal Utility Concept
The system is built for the builder. It should be as automatic as a retail product but as transparent as a development environment.
- **Headless & Automatic**: Starts on boot without interaction.
- **Diagnostic Transparency**: If a component fails, the UI must explain *what* went wrong and provide context (e.g., "Camera disconnected" or "OBD-II Timeout").
- **Durable**: Failure in one module should not crash the entire dashboard.

## 2. Boot Behavior
Upon power-on (vehicle ignition), the system must:
1.  Initialize hardware and networking.
2.  Start the Backend Server.
3.  Report status for each subsystem (Networking, Backend, Cameras, Sensors) to the UI.
4.  *The UI should show a "System Initializing" checklist if boot takes more than a few seconds.*

## 3. Resilience & Partial Failure
The system must be modular enough to survive individual component failures:
- **Component Isolation**: If the Rear Camera fails, the Forward View and Telemetry must keep working.
- **Restart Policies**: Services should attempt to restart, but after 3 failed attempts, they should enter a "Degraded Mode" and report the error to the dashboard.
- **Actionable Logs**: Logs should be accessible via the web UI for quick debugging without needing SSH.
- **Health reporting**: Every major subsystem must have a status: `ACTIVE`, `WAITING`, `FAULTY`, or `DISABLED`.

## 4. Diagnostics & Observability
The dashboard is the primary diagnostic terminal:
- **Status Dashboard**: A dedicated view showing the "Health" of every internal service.
- **Error Breakdown**: Instead of generic "Error," show "Backend API unreachable" or "I2C Sensor Read Failed."
- **System Stats**: CPU temp, RAM usage, and Uptime to monitor Pi health.

---

## Utility Rules

1.  **No Silent Failure**: If it's broken, tell the user *what* is broken.
2.  **Modular Survival**: One broken sensor/camera cannot take down the whole UI.
3.  **Boot Status**: Show exactly where the system is during the startup sequence.
4.  **Web-First Debugging**: Aim to diagnose 90% of issues through the dashboard before reaching for SSH.
5.  **Offline-By-Default**: All intelligence must exist on the Pi; a lack of internet is a normal state, not an error.
6.  **Persistent Status**: Always show the current connection and system health in a corner of the screen.
7.  **Safe Failover**: If a camera stream dies, replace it with a "Sensor Offline" graphic, don't leave a broken <img> tag.
