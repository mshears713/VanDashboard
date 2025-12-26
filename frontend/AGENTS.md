# Frontend Agent Guide: High-Visibility HUD & Diagnostics

The frontend is the primary user interface and diagnostic terminal. It must remain functional even when the backend is struggling.

## 1. UI Resilience (Hard Rule)

- **Ghosting Prevention**: If telemetry data stops flowing, the UI must visually indicate "Stale Data" (e.g., dimming the gauge) rather than showing a frozen 60mph value.
- **Async Loading**: Load video streams and data panels independently. A hanging camera stream must not prevent the speedometer from updating.
- **Placeholder Graphics**: Instead of a "broken image" icon, use a styled "Camera Link Lost" graphic with a "Retry" button.

## 2. High-Visibility Design

Since this is used in a vehicle:
- **Contrast**: Use high-contrast color palettes (OLED-friendly dark modes).
- **Touch Targets**: Ensure buttons (especially "Switch View" or "Shutdown") are large and easy to hit in a moving vehicle.
- **State Feedback**: Use subtle animations or color shifts to indicate that the system is "Alive" (e.g., a heartbeat pulse on the health icon).

## 3. Diagnostic HUD

The UI is a build tool.
- **Persistent Health Bar**: A small, unobtrusive bar showing the colored status (Green/Yellow/Red) of the Backend, Networking, Cameras, and OBD-II.
- **The "Diagnostic Inspector"**: A hidden or secondary view that displays the raw error messages from the Backend Health API (e.g., "Rear Cam: /dev/video1 not found. Check cable.").

## 4. Agent Coding Standards
- **Component Modularity**: Every gauge or camera view should be a self-contained component.
- **Error Boundaries**: Wrap major UI sections in error boundaries to prevent a single JS error from blanking the entire screen.
- **Local State**: Store UI preferences (e.g., brightness, layout) in `localStorage`.

---
*Reference: [docs/AGENTS.md](../docs/AGENTS.md) for the "Personal Utility" philosophy.*
