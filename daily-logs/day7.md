# Day 7 — Multi-User Management & File Isolation

**Date:** 5 July 2026
**Duration:** 15 min
**Topic:** `useradd`, `passwd`, `su`, multi-user security

## Goal
Create isolated users and enforce file-level isolation using `chown` and `chmod 600` — mimicking how AWS EC2 runs each service under its own dedicated user (`www-data`, `mysql`, `appuser`).

## What I Did
- Created a `developer` user with a home directory and bash shell
- Locked `/tmp/dev-secret.txt` to `developer:developer` with `chmod 600`
- Verified isolation: `engineer` got **Permission denied** reading the file; switching to `developer` via `su` read it successfully
- Confirmed multi-user isolation works as intended

## Security Test Performed
| Test | User | Result |
|---|---|---|
| Read `/tmp/dev-secret.txt` | engineer | Permission denied (expected — proves `rw-------` works) |
| Read `/tmp/dev-secret.txt` | developer | Success |

**Result:** File isolation verified — `engineer` cannot read `developer`'s private file.

## Commands Learned
```
sudo useradd -m -s /bin/bash username   # create user + home + shell
sudo passwd username                    # set password for user
sudo su - username                      # switch to user with their environment
whoami                                  # confirm current user
cat /etc/passwd | grep username         # check user exists + shell
ls /home                                # list home directories
```

## Errors Hit & Lessons
1. `useradd: user 'developer' already exists` → not an error — confirms a previous run succeeded
2. Permission denied on `/tmp/dev-secret.txt` as `engineer` → expected, proves the permission model works
3. `/bin/bash/` (trailing slash) and `/bin/bask` typos when creating `appuser` → fixed with `sudo usermod -s /bin/bash appuser`
4. `chown /var/www/myapp: No such file` → folder didn't exist yet; lesson: `ls` before `chown`

## Rule
Create a user with `useradd -m -s /bin/bash`. Always set the password before `su`. `rw-------` means **only** that UID can read the file. `/etc/passwd` is the user database. Always `ls` before `chown`/`chmod` to confirm the path exists.

## AWS Tie-In
This is how EC2 isolates `appuser`, `mysql`, and `www-data`. If one application is compromised, the others stay safe — the same principle used to deploy code without granting developers root access.

**Snapshot:** `Day7-multiuser-complete-with-typo-lesson`
