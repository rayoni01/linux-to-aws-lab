# Day 5 — File Permission Modes (chmod)

**Date:** 1 July 2026

## What I Did
Set `app.log` to `rw-------` using `chmod 600`, and made an executable script using `chmod 755`.

## What Confused Me
- A typo (`apps.log` instead of `app.log`) initially caused "file not found" errors — resolved by checking with `ls`
- Confusion between `./` (current directory) and `~/` (home directory) paths

## Commands Learned
```
chmod 600   # owner: read/write, group: none, others: none
chmod 755   # owner: read/write/execute, group/others: read/execute
ls -l       # verify current permissions
```

## Errors Hit & Fixes
| Error | Fix |
|---|---|
| "No such file" (x2) | Checked actual filename/path with `ls`; stopped mixing `./` and `~/` |

## Rule
Permission digits: `6 = rw-`, `7 = rwx`, `5 = r-x`, `0 = ---`. The three digits in a `chmod` command always represent **owner, group, others** in that order.
