# System Architecture: VanDashboard Topology

This document describes the high-level system design and data flow for the vehicle dashboard.

## 1. Physical Topology

The system operates as a **local hub** with no external internet requirement.

- **Raspberry Pi (The Hub)**:
  - **Networking**: Acts as a Wi-Fi Access Point (AP) or a client on a local vehicle router.
  - **Storage**: SSD or high-endurance SD card holding the OS, backend, and static frontend.
  - **Inputs**: 
    - USB/CSI Cameras (Front/Rear).
    - USB/Bluetooth OBD-II Adapter.
    - Optional I2C/SPI sensors (GPS, Accelerometer).
- **Android Phone (The Display)**:
  - Connects to the Pi's Wi-Fi.
  - Views the dashboard via a standard web browser (Chrome/Edge).

## 2. Software Stack

- **Backend**: Python (FastAPI/Flask) or Node.js (Express).
  - Handles hardware polling and video stream piping.
  - Serves the compiled frontend.
- **Frontend**: TypeScript + Modern Framework (React/Vite).
  - Responsive layout for mobile/tablet.
  - WebSocket/SSE for real-time telemetry.

## 3. Data Flow

1.  **Hardware Polling**: Backend polls OBD-II and sensors at 1–10Hz.
2.  **Streaming**: Camera frames are piped to the client with minimal latency.
3.  **Consumption**: Frontend renders gauges and video feeds, providing diagnostic feedback.

---
*Reference: [RUNTIME_MODEL.md](RUNTIME_MODEL.md) for operational behavior.*
