# 🔓 Level 22 → Level 23 — Cron Jobs and Script Analysis

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit22` |
| **Password** | `tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q` (from Level 21) |

---

## 🎯 Challenge

> A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.
>
> **NOTE:** Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

**Commands you may need:** `cron`, `crontab`, `crontab(5)` (use "man 5 crontab" to access this)

---

## 🧠 Understanding the Challenge

This level builds on the previous cron job concept, but requires analyzing a shell script that creates temporary files.

### The Approach

1. Find the cron job for bandit23 in `/etc/cron.d/`
2. Examine the script it runs
3. Understand what the script does
4. Find where the script writes the password or output

### Script Analysis Skills

When analyzing unknown scripts, look for:
- Where files are created or written to
- What commands are executed
- Where output is redirected
- Variable values and expansions

---

## 💡 Solution

### Step 1: Connect to Level 22

```bash
ssh bandit22@bandit.labs.overthewire.org -p 2220
