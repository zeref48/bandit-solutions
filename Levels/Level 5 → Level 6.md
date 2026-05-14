# 🔓 Level 5 → Level 6 — Finding Files by Properties

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit5` |
| **Password** | `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw` (from Level 4) |

---

## 🎯 Challenge

> The password for the next level is stored in a file somewhere under the **inhere** directory and has all of the following properties:
> - human-readable
> - 1033 bytes in size
> - not executable

**Commands you may need:** `ls`, `cd`, `cat`, `file`, `du`, `find`

---

## 🧠 Understanding the Challenge

This level introduces the powerful `find` command with multiple search criteria.

### The `find` Command

The `find` command searches for files and directories based on various properties:

```bash
find [path] [criteria] [action]
