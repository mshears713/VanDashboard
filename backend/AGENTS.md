# Backend Agent Guide: Resilience & Hardware Orchestration

The backend is the engine of the VanDashboard. It must be robust against hardware instability and provide crystal-clear diagnostics to the frontend.

## 1. Modular Survival (Hard Rule)

Each hardware interface (OBD-II, Camera 1, Camera 2, GPS) must be treated as a **volatile dependency**.
- **Independant Lifecycle**: The failure to initialize one hardware component must not block the initialization of others. For example, if the Rear Camera doesn't find `/dev/video1`, the Front Camera on `/dev/video0` must still start.
- **Graceful Retries**: Implement exponential backoff for hardware re-connection attempts. After a set number of failures, notify the Health API.

## 2. The Health API Strategy

The backend must maintain a global "State Machine" of all subsystems.
- **Status Codes**: 
  - `OK`: Running and producing valid data.
  - `WAITING`: Initializing or retrying connection.
  - `FAULT`: Hardware found but producing errors (e.g., checksum parity error).
  - `DISABLED`: Not found or explicitly turned off.
- **Verbose Error Payload**: Include the *exact* system error (e.g., "Permission Denied", "No such device") in the API response so the UI can display it.

## 3. Data Streaming & Performance

- **Video Piping**: Use low-latency formats (MJPEG for initial simplicity, or HLS/WebRTC for performance). Avoid heavy transcoding on the Pi CPU.
- **Telemetry Frequency**: Target 5–10Hz for smooth gauge movement. Batch updates to reduce network overhead if necessary.

## 4. Networking Modes
- **Mode Management**: The backend must handle the transition logic between Vehicle (AP) and Maintenance (Station) modes.
- **Auto-Reversion**: If switching to Maintenance Mode fails, the backend must ensure the system returns to a working Vehicle Mode.
- **Port Consistency**: Ensure the API and static server remain on the same ports across mode shifts.

## 5. Agent Coding Standards
- **Logging**: Use a structured logger. Include timestamps and module tags.
- **Safety**: Use `try/except` or `try/catch` blocks around all I/O operations.
- **SD Card Health**: Minimize frequent small writes. Buffer logs and flush them periodically or rotate them aggressively.

---
*Reference: [docs/RUNTIME_MODEL.md](../docs/RUNTIME_MODEL.md) for recovery policies.*
