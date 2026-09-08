# Day 8 — Groups & Secure Shared Access

**Date:** 6 July 2026
**Duration:** 20 min
**Topic:** `groupadd`, `usermod -aG`, `chgrp`, group permissions

## Goal
Replace insecure `chmod 777` sharing with group-based access. Create a `devops` group, add both `engineer` and `developer` to it, and create a file owned by `engineer:devops` with `640` permissions.

**AWS Equivalent:** Adding `ubuntu` and `deploy` users to the `www-data` group to safely share `/var/www/html`.

## What I Did
- Created the `devops` group
- Added both `engineer` and `developer` to it with `usermod -aG`
- Created `/tmp/team.txt`, set ownership to `engineer:devops`, permissions to `640`
- Verified group-based read access works as intended

## Commands Learned
```
sudo groupadd groupname          # create group
sudo usermod -aG group username  # add user to group (-a = append, don't replace)
groups                           # show current user's groups
groups username                  # show another user's groups
sudo chown :groupname file       # change group ownership only
sudo chmod 640 file              # owner rw, group r, others none
```

## Verification Tests
| Test | Result |
|---|---|
| `engineer` reads `/tmp/team.txt` | Success (owner `rw-`) |
| `developer groups` (before session reload) | Only shows `developer` — group not yet loaded |
| `developer groups` (after `sudo su - developer`) | Shows `developer devops` — correct |
| `developer` reads `/tmp/team.txt` (before reload) | Permission denied — groups hadn't reloaded |
| `developer` reads `/tmp/team.txt` (after reload) | Success — "DevOps team notes" |
| Typo test: `cat /tmp.team.txt` | No such file — confirms typos cause a large share of real permission tickets |

## Critical Lessons Learned
1. `usermod -aG` **requires** `-a` (append) — without it, the user is removed from all other groups, including `sudo`
2. Group membership only loads at login — use `sudo su - username` or a fresh login for new groups to apply
3. `/tmp` clears on reboot — never store important evidence there; use a persistent directory like `~/lab`
4. `640` permissions (owner rw, group r, others none) enable secure team sharing and pass SOC2-style scrutiny — `777` does not

## AWS Tie-In
This mirrors how `ubuntu` and `appuser` share `/var/www` via the `www-data` group — used instead of `chmod 777` specifically for compliance reasons (e.g. SOC2).

**Snapshot:** `Day8-groups-devops-640-working`
