# 🔓 Level 19 → Level 20 — Using setuid Binaries

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit19` |
| **Password** | `cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8` (from Level 18) |

---

## 🎯 Challenge

> To gain access to the next level, you should use the **setuid binary** in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

**Helpful Reading Material:**
- [setuid on Wikipedia](https://en.wikipedia.org/wiki/Setuid)

---

## 🧠 Understanding the Challenge

This level introduces the concept of **setuid binaries** (Set User ID).

### What is setuid?

setuid is a special permission that allows a program to run with the privileges of the **file owner**, not the user who executes it.

| Normal Program | setuid Program |
|----------------|----------------|
| Runs as the user who executes it | Runs as the file owner |
| Can only access what the user can access | Can access what the owner can access |
| Example: `ls` runs as you | Example: `passwd` runs as root |

### Viewing setuid permissions

```bash
ls -l filename
