# 🔓 Level 12 → Level 13 — Hex Dumps and Repeated Compression

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit12` |
| **Password** | `7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4` (from Level 11) |

---

## 🎯 Challenge

> The password for the next level is stored in the file **data.txt**, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command "mktemp -d". Then copy the datafile using cp, and rename it using mv (read the manpages!)

**Commands you may need:** `grep`, `sort`, `uniq`, `strings`, `base64`, `tr`, `tar`, `gzip`, `bzip2`, `xxd`, `mkdir`, `cp`, `mv`, `file`

**Helpful Reading Material:**
- [Hex dump on Wikipedia](https://en.wikipedia.org/wiki/Hex_dump)

---

## 🧠 Understanding the Challenge

This level involves multiple steps of decompression and introduces several important commands.

### Key Concepts

| Concept | Explanation |
|---------|-------------|
| **Hex dump** | A representation of binary data in hexadecimal format |
| **`xxd` command** | Creates hex dumps and reverses them (convert hex back to binary) |
| **`file` command** | Identifies file types (compressed, tar, etc.) |
| **`mv` command** | Renames or moves files |
| **`cp` command** | Copies files |
| **Working in /tmp** | Avoid cluttering your home directory |

### Common Compression Formats

| Extension | Format | Decompression Command |
|-----------|--------|----------------------|
| `.gz` | gzip | `gunzip file.gz` or `gzip -d file.gz` |
| `.bz2` | bzip2 | `bunzip2 file.bz2` or `bzip2 -d file.bz2` |
| `.tar` | Tape archive | `tar xf file.tar` |
| `.zip` | Zip | `unzip file.zip` |

### The Process

1. Create a working directory in `/tmp`
2. Copy `data.txt` to the working directory
3. Reverse the hex dump to get the original binary file
4. Identify the compression type using `file`
5. Decompress repeatedly until you get a text file
6. The password will be in the final decompressed file

---

## 💡 Solution

### Step 1: Connect to Level 12

```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
