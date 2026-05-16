# 🔓 Level 9 → Level 10 — Finding Human-Readable Strings

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit9` |
| **Password** | `4CKMh1JI91bUIZZPXDqGanal4xvAg0JM` (from Level 8) |

---

## 🎯 Challenge

> The password for the next level is stored in the file **data.txt** in one of the few human-readable strings, preceded by several ‘=’ characters.

**Commands you may need:** `grep`, `sort`, `uniq`, `strings`, `base64`, `tr`, `tar`, `gzip`, `bzip2`, `xxd`

---

## 🧠 Understanding the Challenge

This level introduces the `strings` command, which extracts human-readable text from binary files.

### The `strings` Command

`strings` finds and prints printable character sequences in files:

```bash
strings [options] [file]
