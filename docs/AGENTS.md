# Docs Agent Guide: Master Blueprint & Engineering Strategy

This guide defines the core philosophies and architectural standards that govern the entire VanDashboard project. As an agent, follow these principles when making high-level design decisions.

## 1. Core Philosophies

### A. The "Personal Utility" Model
We are not building a consumer product for the masses; we are building a high-precision tool for an owner-builder.
- **Transparency over Simplicity**: Do not hide errors behind generic "Oops" messages. Show technical detail (e.g., "Serial Timeout on /dev/ttyUSB0") so the user can fix the hardware.
- **Resilience through Modality**: The system must be "partially functional" at all times. The failure of a non-critical module (like a backup camera) must never prevent the telemetry display from working.

### B. Offline-First "Appliance" Design
The Raspberry Pi is a vehicle appliance.
- **Zero-Config Startup**: Every service required for a "safe drive" must start automatically on boot.
- **No Internet Dependency**: The system must provide its full core value (cameras, gauges, diagnostics) without a cloud connection.

## 2. System Topology & Data Flow

- **The Hub (Raspberry Pi)**:
  - **Networking**: Handles the local Wi-Fi AP. It is the single source of truth for telemetry.
  - **Backend**: Acts as a greedy orchestrator. It polls hardware, buffers video, and serves the static frontend.
- **The Client (Android Phone)**:
  - **Browser-Based**: No native app requirement. The UI must be optimized for mobile web browsers, focusing on touch targets and visibility in varying light conditions.

## 3. Engineering Workflows

- **WSL as the Lab**: All code logic is validated in WSL using mock hardware signals.
- **Pi as the Field**: Final integration and hardware-specific debugging happen on the Pi via SSH/Dashboard.
- **Git Handoff**: GitHub is the bridge between the labs (WSL) and the field (Pi).

## 4. Operating Modes
- **Vehicle Mode (Default)**: Pi as Access Point, offline, high reliability.
- **Maintenance Mode**: Pi as Station, online, used for updates.
- **Safety Rule**: Always revert to Vehicle Mode on boot or if Maintenance Mode connection fails to prevent lockouts.

## 5. Agent Checklist for New Docs
- [ ] Does this document align with the "Personal Utility" model?
- [ ] Is the terminology implementation-agnostic where possible?
- [ ] Are links to other `AGENTS.md` files included for context?
