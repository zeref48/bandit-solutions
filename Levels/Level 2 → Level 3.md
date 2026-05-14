# 🔓 Level 2 → Level 3 — Spaces in Filename

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit2` |
| **Password** | `263JGJPfgU6LtdEvgfWU1XP5yac29mFx` (from Level 1) |

---

## 🎯 Challenge

> The password for the next level is stored in a file called **spaces in this filename** located in the home directory.

**Commands you may need:** `ls`, `cd`, `cat`, `file`, `du`, `find`

---

## 🧠 Understanding the Challenge

The challenge here is that the filename contains **spaces**.

### Why is this tricky?

In Linux, spaces are used as **delimiters** between command arguments. When you type:

```bash
cat spaces in this filename
```
The shell interprets this as:

  - cat (command)

  - spaces (first argument - a file named "spaces")

  - in (second argument - a file named "in")

  - this (third argument - a file named "this")

  - filename (fourth argument - a file named "filename")

It thinks you're trying to cat four separate files — not one file with spaces in its name.
