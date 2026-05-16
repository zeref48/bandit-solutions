# 🔓 Level 8 → Level 9 — Finding Unique Lines with sort and uniq

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit8` |
| **Password** | `dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc` (from Level 7) |

---

## 🎯 Challenge

> The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only once

**Commands you may need:** `grep`, `sort`, `uniq`, `strings`, `base64`, `tr`, `tar`, `gzip`, `bzip2`, `xxd`

**Helpful Reading Material:**
- [Piping and Redirection](https://www.gnu.org/software/bash/manual/html_node/Redirections.html)

---

## 🧠 Understanding the Challenge

This level introduces the `sort` and `uniq` commands, which are essential for finding unique or duplicate lines in files.

### The `sort` Command

`sort` arranges lines in alphabetical or numerical order:

```bash
sort [options] [file]
