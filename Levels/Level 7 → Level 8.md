# 🔓 Level 7 → Level 8 — Searching Within Files with grep

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit7` |
| **Password** | `morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj` (from Level 6) |

---

## 🎯 Challenge

> The password for the next level is stored in the file **data.txt** next to the word **millionth**

**Commands you may need:** `man`, `grep`, `sort`, `uniq`, `strings`, `base64`, `tr`, `tar`, `gzip`, `bzip2`, `xxd`

---

## 🧠 Understanding the Challenge

This level introduces the `grep` command, one of the most powerful tools for searching within files.

### The `grep` Command

`grep` (Global Regular Expression Print) searches for patterns in files:

```bash
grep [options] pattern [file]
