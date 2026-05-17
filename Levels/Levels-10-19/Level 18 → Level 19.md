# 🔓 Level 18 → Level 19 — Escaping a Restricted Shell

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit18` |
| **Password** | `x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO` (from Level 17) |

---

## 🎯 Challenge

> The password for the next level is stored in a file **readme** in the homedirectory. Unfortunately, someone has modified **.bashrc** to log you out when you log in with SSH.

**Commands you may need:** `ssh`, `ls`, `cat`

---

## 🧠 Understanding the Challenge

This level demonstrates how to bypass a restricted shell that logs you out immediately.

### The Problem

When you try to log in normally:

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220
