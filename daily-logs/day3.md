# Day 3 — Permissions & sudo Basics

**Date:** 30 June 2026

## What I Did
Created and deleted files in `/root` using `sudo`, and learned why folder permissions block plain `ls` for non-root users.

## What Confused Me
The difference between `ls -l` and `ls -1`, and why I still couldn't read `/root` even after creating a file there myself.

## Commands Learned
```
sudo        # run a command with elevated privileges
ls -l       # list with permission/ownership detail
touch       # create an empty file
rm          # remove a file
```

## Errors Hit & Fixes
| Error | Fix |
|---|---|
| Permission denied on `touch /root/...` | Used `sudo touch` |
| Permission denied on `ls /root` | Used `sudo ls` |

## Rule
`sudo` is required for *each* protected action individually — it doesn't grant standing elevated access for the rest of the session.
