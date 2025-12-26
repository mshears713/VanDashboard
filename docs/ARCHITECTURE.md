# System Architecture

## Topology

- **Raspberry Pi (Hub)**:
  - Acts as a local Wi-Fi Access Point (AP).
  - Hosts the Backend Server (Handles API requests, camera streams, and serves static frontend files).
  - Connects to hardware (Cameras via USB/CSI, OBD-II via Bluetooth).
- **Android Phone (Client)**:
  - Connects to the Pi's Wi-Fi network.
  - Opens a web browser to the Pi's local IP (e.g., `http://192.168.4.1`).

## Data Flow

1. **User Interaction**: Phone browser sends requests to Backend.
2. **Telemetry**: Backend polls OBD-II/GPS and pushes data to Frontend via WebSockets or polling.
3. **Video**: Backend pipes camera streams directly to the browser.

## Deployment Model

The Pi runs as a headless system. Services are managed via `systemd`.
