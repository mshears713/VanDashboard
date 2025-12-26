# System Operating Modes

The VanDashboard operates in two distinct networking states to balance localized reliability with the occasional need for updates.

## 1. Mode 1: Vehicle Mode (Default / Appliance)
This is the primary state when the van is in operation.
- **Networking**: The Pi acts as its own **Wi-Fi Access Point (AP)**.
- **Connectivity**: The Android phone joins the "VanDashboard" network.
- **Internet**: Assuming **Offline**.
- **Update Ability**: None.
- **Primary Goal**: Immediate, zero-latency access to cameras and sensors without dependency on external signals.

## 2. Mode 2: Maintenance Mode (On-Demand / Service)
Used for software updates, installing new dependencies, or remote debugging.
- **Networking**: The Pi switches to **Wi-Fi Station Mode**.
- **Connectivity**: The Pi joins an external network (e.g., your phone's Wi-Fi hotspot or a home router).
- **Internet**: **Online**.
- **Update Ability**: `git pull`, `apt update`, `npm install` are functional.
- **Primary Goal**: Connect the "Appliance" to the outside world for maintenance.

---

## 3. System Invariants (What Never Changes)
Regardless of the network mode, the following must remain constant to prevent user confusion:
- **Core Services**: The backend and frontend servers MUST stay running.
- **Service Ports**: The dashboard must always be on the same port (e.g., `:80` or `:3000`).
- **Local API**: All telemetry and camera endpoints must function normally (though they may be accessed via a different IP).
- **Boot Default**: The system must always boot into **Vehicle Mode** unless explicitly commanded otherwise.

---

## 4. Mode Switch Contract

### User Experience
1.  User clicks "Enable Maintenance Mode" on the Dashboard.
2.  Dashboard warns: "This will temporarily disconnect your current session."
3.  Pi attempts to join the predefined "Maintenance Hotspot."

### Identifying the Current Mode
The dashboard status bar must explicitly show:
- **Mode Name**: `Vehicle` vs `Maintenance`.
- **Local IP Address**: So the user knows which URL to use if the discovery fails.
- **Internet Status**: Signal strength or "Offline" icon.

### Failure Handling
- **The "Safety Net"**: If the Pi fails to join the Maintenance hotspot within 60 seconds, it must automatically kill the attempt and revert to **Vehicle Mode** (AP mode).
- **Recovery**: The user should never be "locked out" of the Pi because of a bad Wi-Fi password in Maintenance Mode.
