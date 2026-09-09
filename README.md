# Linux to AWS DevOps Journey — Cloud Foundations Lab

A self-directed, 180-day hands-on lab building Linux systems administration skills from the ground up, with every concept explicitly tied back to how it plays out in AWS production environments.

**Why this exists:** SIEM/EDR alerts and cloud security incidents are only as good as the analyst's understanding of the systems underneath them. This lab is my way of building that understanding from first principles — installing, breaking, and fixing real systems — rather than only working from dashboards.

## Environment

- Oracle VirtualBox — Ubuntu 24.04 LTS (initial build) / Ubuntu 22.04 LTS (lab VM)
- 2 CPU, 4GB RAM, 50GB disk
- VirtualBox snapshots used as rollback checkpoints (the local analogue to AWS EBS snapshots)

## Structure

```
/daily-logs/     Day-by-day journal — commands, errors, fixes, and the AWS tie-in for each concept
/scripts/        Any scripts or configs produced along the way
README.md        This file
```

## Progress So Far

| Day | Topic | Key Skills |
|---|---|---|
| 1 | Linux install & recovery | VM setup, driver troubleshooting, snapshot-based recovery |
| 2–4 | Terminal fundamentals | `pwd`, `ls`, `cd`, `mkdir`, `sudo`, package management (`apt`) |
| 5–6 | File permissions & ownership | `chmod`, `chown`, permission model (owner/group/others) |
| 7 | Multi-user isolation | `useradd`, `passwd`, `su`, verified access isolation between users |
| 8 | Group-based access control | `groupadd`, `usermod -aG`, `chmod 640`, replacing `chmod 777` with least-privilege sharing |
| 9 | Troubleshooting fundamentals *(in progress)* | `find`, `grep`, `ps`, `kill` — disk, log, and process triage |

## Why It Matters (AWS Relevance)

Every exercise is deliberately mapped to a real AWS/production pattern:

- **User & permission isolation** → how AWS EC2 separates service accounts (`www-data`, `mysql`, `appuser`) so a compromise in one doesn't cascade
- **Group-based sharing (640, not 777)** → the same least-privilege model used for shared web app directories (`/var/www/html`) across multiple service users
- **Snapshots** → the same recovery discipline as AWS EBS snapshots for rolling back a broken instance
- **`find` / `grep` / `ps` triage** → the actual first-response toolkit for common ops tickets: disk-full, app crash logs, high-CPU processes

## Methodology

Each day is logged with a consistent structure: what I did, what confused me, what clicked, commands learned, errors hit and how I fixed them, and a verification/security test where relevant. Security controls aren't just applied — they're deliberately broken and tested (e.g., confirming a locked-down file is genuinely unreadable by another user) before being marked complete.

## Roadmap

- Days 10–14: filesystem deep-dive (`df`, `du`, `ln -s`, `tar`), user/group cleanup
- Day 15: Nginx installation and a real deployment under `/var/www`
- Day 16+: Docker and container-level permission management

---
*Part of an ongoing self-directed learning programme alongside my work in SOC operations and incident response. See also: [canary-token-detection-lab](#) for deception-technology and detection-engineering work.*
