# 🔓 Level 3 → Level 4 — Hidden Files

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit3` |
| **Password** | `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx` (from Level 2) |

---

## 🎯 Challenge

> The password for the next level is stored in a hidden file in the **inhere** directory.

**Commands you may need:** `ls`, `cd`, `cat`, `file`, `du`, `find`

---

## 🧠 Understanding the Challenge

In Linux, **hidden files** are files that start with a dot (`.`). 

### What are hidden files?

| File | Hidden? | How to see |
|------|---------|------------|
| `readme` | No (visible) | `ls` |
| `.hidden` | Yes (hidden) | `ls -la` or `ls -a` |
| `.bashrc` | Yes (hidden) | `ls -la` |
| `..` | Special (parent directory) | `ls -la` |
| `.` | Special (current directory) | `ls -la` |

### How to see hidden files

| Command | Shows |
|---------|-------|
| `ls` | Only non-hidden files |
| `ls -a` | All files (including hidden, `.`, and `..`) |
| `ls -la` | All files with detailed information (permissions, size, etc.) |

### The `-a` flag

`-a` stands for **"all"** — it shows everything, including hidden files.
