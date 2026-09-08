# Day 2 — Terminal Basics

**Date:** 30 June 2026

## What I Did
Created my first folder and file using only the terminal — no GUI file manager.

## What Confused Me
`mkdir` requires a space between the command and the folder name — running it without one just looks like an unrecognized command.

## Commands Learned
```
pwd       # print working directory
ls        # list directory contents
cd        # change directory
mkdir     # make a new directory
echo >    # write text into a file
cat       # print file contents
```

## Errors Hit & Fixes
| Error | Fix |
|---|---|
| `mkdir-projects: command not found` | Missing space — corrected to `mkdir cloud-projects` |

## Rule
Every command and its arguments need a space between them — there's no implicit separator in the shell.
