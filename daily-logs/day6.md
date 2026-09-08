# Day 6 — Ownership (chown)

**Date:** 1 July 2026

## What I Did
Used `chown` to change `app.log`'s ownership to `root:root`, confirmed that reading it as `engineer` then failed, read it successfully with `sudo`, then reverted ownership back.

## What Confused Me
Nothing major — carried forward the `~/` full-path lesson from Day 5 without issue this time.

## Commands Learned
```
sudo chown user:group <file>   # change file ownership
cat / sudo cat                 # read a file (with or without elevated access)
cd, ls -l                      # navigate and verify ownership/permissions
```

## Errors Hit & Fixes
| Error | Fix |
|---|---|
| Permission denied reading `app.log` as `engineer` after ownership change | Used `sudo cat` |

## Rule
To read a file, you must be the owner, be in a group with read access, or have "others" read access granted — otherwise it's Permission denied regardless of who you are. `chown` itself requires `sudo` to run. A `600` file is only truly private if its owner is set correctly — otherwise even the "owner" permission bits are meaningless to you.
