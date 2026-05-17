# 🔓 Level 21 → Level 22 — Cron Jobs

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit21` |
| **Password** | `EeoULMCra2q0dSkYj561DX7s1CpBuOBt` (from Level 20) |

---

## 🎯 Challenge

> A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.

**Commands you may need:** `cron`, `crontab`, `crontab(5)` (use "man 5 crontab" to access this)

---

## 🧠 Understanding the Challenge

This level introduces **cron**, the time-based job scheduler in Linux.

### What is Cron?

Cron is a daemon that executes scheduled commands at specific times or intervals. It's used for:
- Automated backups
- System maintenance tasks
- Running scripts periodically

### Cron Configuration Locations

| Location | Purpose |
|----------|---------|
| `/etc/crontab` | System-wide crontab file |
| `/etc/cron.d/` | Directory for individual cron job files |
| `/etc/cron.hourly/` | Scripts run every hour |
| `/etc/cron.daily/` | Scripts run every day |
| `/etc/cron.weekly/` | Scripts run every week |
| `/etc/cron.monthly/` | Scripts run every month |
| `crontab -e` | User-specific crontab (editable) |

### Crontab Syntax
