# Day 4 — Package Management

**Date:** 30 June 2026

## What I Did
Installed my first package (`tree`) using `apt`, running an update first.

## What Confused Me
Nothing major — the distinction between updating package lists and actually installing a package was clear from the start.

## Commands Learned
```
sudo apt update            # refresh available package lists
sudo apt install <package> # install a package
tree                        # visualize directory structure
```

## Errors Hit & Fixes
None. An `autoremove` suggestion for `libfwupd2` appeared but was safely ignored — it's a routine cleanup hint, not an error.

## Rule
Always run `apt update` before `apt install` — installing against a stale package list can pull outdated or missing packages. The `-y` flag skips the interactive Y/n confirmation prompt.
