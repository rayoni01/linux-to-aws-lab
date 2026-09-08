# Day 9 — Find, Grep, Ps: Troubleshooting Fundamentals (In Progress)

**Topic:** Locating files, searching inside files, and managing processes — core support/triage skills.

## Goal
Learn the fundamental troubleshooting toolkit for common operational issues: disk usage, log searching, and process management.

## Commands Introduced
```
mkdir -p ~/lab/day9                       # persistent lab directory (not /tmp)
find [path] -name pattern                 # locate files by name
find ~ -type f -size +1M 2>/dev/null      # find large files, suppressing permission errors
grep -r text folder                       # search recursively for text inside files
grep -i case-insensitive                  # case-insensitive search
ps aux                                    # list all running processes
ps aux | grep process                     # filter processes by name
sleep 300 &                               # run a background process for testing
kill PID                                  # terminate a process gracefully
kill -9 PID                               # force-terminate a process
```

## Real-World Tickets This Solves
| Scenario | Approach |
|---|---|
| Disk full | `find` for large log files eating space |
| Application crashing | `grep ERROR /var/log/...` to trace the failure |
| High CPU usage | `ps aux` to identify the process, `kill` to stop it |

## Notes
This continues the lesson from Day 8 — using `~/lab` rather than `/tmp` for anything meant to persist across reboots.

**Status:** In progress.
