# Config Agent Guide: Environment & System Stability

This folder stores the templates and settings required for the Pi's operational environment.

## 1. Environment Management

- **External vs. Internal**: Use `.env.example` files to define required variables (API keys, ports, device paths).
- **No Secrets in Git**: Never commit active `.env` files or hardware-specific MAC addresses.

## 2. Infrastructure Configs

- **systemd**: Store `.service` templates here for auto-starting the backend.
- **Networking**: Store templates for `hostapd` (Wi-Fi AP) and `dnsmasq` to ensure the Pi starts its own network correctly.
- **FS Settings**: Templates for `fstab` or other OS settings that ensure the SD card is treated with care (e.g., using `noatime`).

## 3. Agent Rules
- **Template First**: When adding a new config requirement, always create a documented `.example` or `.template` file first.
- **Comments**: Every setting in a config file should have a comment explaining its purpose in the context of the Van appliance.

---
*Reference: [docs/AGENTS.md](../docs/AGENTS.md) for the "Appliance" design rules.*
