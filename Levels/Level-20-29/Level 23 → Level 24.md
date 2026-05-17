# 🔓 Level 23 → Level 24 — Creating Your Own Shell Script

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit23` |
| **Password** | `0Zf11ioIjMVN551jX3CmStKLYqjk54Ga` (from Level 22) |

---

## 🎯 Challenge

> A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.
>
> **NOTE:** This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!
>
> **NOTE 2:** Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

**Commands you may need:** `chmod`, `cron`, `crontab`, `crontab(5)` (use "man 5 crontab" to access this)

---

## 🧠 Understanding the Challenge

This level requires you to create a shell script that will be executed by a cron job.

### The Setup

1. There's a cron job that runs a script in `/usr/bin/cronjob_bandit24.sh`
2. That script executes all scripts in `/var/spool/bandit24/` (or similar directory)
3. The cron job runs as `bandit24`
4. We can create a script in that directory that will be executed with bandit24's privileges

### The Goal

Create a script that:
1. Runs with bandit24's permissions
2. Reads the password from `/etc/bandit_pass/bandit24`
3. Saves it somewhere we can access (like `/tmp/`)

### Important Note

The script is removed after execution, so we need to:
- Create our script in the spool directory
- Make it executable
- Have it write the password to a location we control

---

## 💡 Solution

### Step 1: Connect to Level 23

```bash
ssh bandit23@bandit.labs.overthewire.org -p 2220
