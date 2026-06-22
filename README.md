# Klipper Config — Ender 3 Pro

My configuration for a Creality Ender 3 Pro running the **Klipper** firmware stack on a Raspberry Pi 4. This is config-as-code: the printer's behavior, calibration, and macros all live in version-controlled text files rather than being clicked into a UI.

> **Note:** secrets and network details are intentionally excluded. `cors_domains` / `trusted_clients` in `moonraker.conf` are left empty here on purpose — set them to your own network when deploying.

## The stack

| Component | Role |
|-----------|------|
| **Klipper** | Firmware — runs the motion planning and kinematics on the Pi instead of the printer's mainboard |
| **Moonraker** | API server that sits between Klipper and the web UI |
| **Mainsail** | Web interface for control, monitoring, and G-code management |
| **Crowsnest** | Webcam streaming service |
| **Sonar** | Keeps the connection alive / network reliability helper |
| **moonraker-timelapse** | Automated print timelapses |

Hardware: Creality Ender 3 Pro · Raspberry Pi 4 · BLTouch auto bed-leveling probe · USB webcam.

## What's in here

| File | What it is |
|------|-----------|
| `printer.cfg` | The main config — stepper settings, kinematics, probe/BLTouch setup, PID values, custom macros |
| `printer-2026*.cfg` | Timestamped `SAVE_CONFIG` snapshots — the history of calibration as the printer was dialed in (PID tuning, probe offsets) |
| `moonraker.conf` | Moonraker API server config (network fields blanked) |
| `crowsnest.conf` | Webcam streaming config |
| `sonar.conf` | Connection-keepalive config |
| `mainsail.real.cfg` | Mainsail UI macros/config (the resolved file behind the symlink) |
| `timelapse.real.cfg` | Timelapse macro config (the resolved file behind the symlink) |

## Notes

- The `printer-2026*.cfg` files are auto-generated backups Klipper writes whenever `SAVE_CONFIG` runs after a calibration. They're kept here as a record of how the printer was tuned over time.
- This config was salvaged off the SD card after a storm took the Pi down — see [engineering-log entry 002](https://github.com/KD-Acorn/engineering-log/blob/main/002-storm-killed-pi-recovery.md) for that recovery. Having it in version control means the printer can be rebuilt and dialed back in from scratch.

---

Maintained by [Kennedy Durham](https://github.com/KD-Acorn). Part of my [home-lab](https://github.com/KD-Acorn/home-lab).
