# Day 1 — Linux Foundations: Install & Recovery

**Date:** 29 June 2026
**Milestone:** M1 - Linux Foundations

## What I Did
- Created a 50GB Ubuntu 24.04.4 LTS VM in VirtualBox with 2 CPU, 4GB RAM
- Fixed a `vmwgfx` graphics crash by switching to VBoxSVGA with 128MB video memory
- Booted the Ubuntu live desktop and handled the installer update flow
- Debugged an installer that wouldn't launch by running `sudo ubiquity gtk_ui` from the terminal
- Completed the full OS install, creating user `engineer` on host `cloud-lab`
- Verified the install with `whoami`, `lsb_release -ds`, `df -h /`, `uptime`
- Performed a clean shutdown with `sudo poweroff`
- Took a snapshot (`Day1-Clean-Ubuntu`) as a restore point

## What Confused Me
- White screen instead of the installer window after boot
- The "Install Ubuntu" desktop icon not responding to double-click
- `ubiquity` command not found in the terminal after an installer update
- Password prompts showing no dots/stars while typing
- A "Close this terminal?" popup interrupting shutdown

## What Clicked
- VirtualBox graphics drivers matter — Ubuntu 24.04 needs VBoxSVGA, not the default
- In real cloud environments, installer updates are typically skipped and patched post-install (`sudo apt update` after install is the real-world workflow)
- When the GUI breaks, drop to the terminal — `sudo ubiquity` force-launches the installer
- Linux password prompts are intentionally silent — type blind and press Enter
- VirtualBox snapshots are the direct equivalent of AWS EBS snapshots — this is how broken servers get recovered

## Commands Learned
| Command | Purpose |
|---|---|
| `whoami` | Shows current username |
| `lsb_release -ds` | Shows Ubuntu version |
| `df -h /` | Shows disk usage for root partition |
| `uptime` | Shows system uptime and load |
| `sudo poweroff` | Graceful Linux shutdown |
| `sudo ubiquity gtk_ui` | Force-launch the Ubuntu graphical installer |

## Errors Hit & Fixes
| Error | Fix |
|---|---|
| `vmwgfx` unsupported hypervisor warning | Changed VM Display settings to VBoxSVGA, 128MB VRAM |
| Installer opened as a blank/white window | Closed with Alt+F4, relaunched via terminal |
| "Install Ubuntu" icon not responding | Opened terminal (Ctrl+Alt+T), ran `sudo ubiquity gtk_ui` |
| `ubiquity: command not found` | Installer binary missing after update — used direct launch method instead of reinstalling |
| VM wouldn't shut down ("process running" popup) | Cancelled popup, typed password into terminal for `sudo poweroff` |

**Status:** Complete. VM powered off. Snapshot saved.
