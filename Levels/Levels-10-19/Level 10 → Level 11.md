
# 🔓 Level 10 → Level 11 — Decoding Base64

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit10` |
| **Password** | `FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey` (from Level 9) |

---

## 🎯 Challenge

> The password for the next level is stored in the file **data.txt**, which contains base64 encoded data

**Commands you may need:** `grep`, `sort`, `uniq`, `strings`, `base64`, `tr`, `tar`, `gzip`, `bzip2`, `xxd`

**Helpful Reading Material:**
- [Base64 on Wikipedia](https://en.wikipedia.org/wiki/Base64)

---

## 🧠 Understanding the Challenge

This level introduces **Base64 encoding** and the `base64` command to decode it.

### What is Base64?

Base64 is a way to convert binary data into text using only 64 characters (A-Z, a-z, 0-9, +, /). It's commonly used for:
- Sending binary data in emails (attachments)
- Storing binary data in text files
- Encoding credentials in HTTP headers

### Base64 Example

| Text | Base64 Encoded |
|------|----------------|
| `hello` | `aGVsbG8=` |
| `password` | `cGFzc3dvcmQ=` |
| `Bandit` | `QmFuZGl0` |

The `=` at the end is padding to make the length a multiple of 4.

### The `base64` Command

```bash
base64 [options] [file]
```
## 💡 Solution
### Step 1: Connect to Level 10
```bash

ssh bandit10@bandit.labs.overthewire.org -p 2220
```
Password: FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
### Step 2: Check what files are in the home directory
```bash

bandit10@bandit:~$ ls -al
```
Output:
```

total 24
drwxr-xr-x   2 root     root     4096 Apr  3 15:17 .
drwxr-xr-x 150 root     root     4096 Apr  3 15:20 ..
-rw-r--r--   1 root     root      220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root     root     3851 Apr  3 15:10 .bashrc
-rw-r-----   1 bandit11 bandit10   69 Apr  3 15:17 data.txt
-rw-r--r--   1 root     root      807 Mar 31  2024 .profile
```
There's a file named data.txt (69 bytes).
### Step 3: View the encoded data (optional)
```

bandit10@bandit:~$ cat data.txt
```
Output:
```

VGhlIHBhc3N3b3JkIGlzIGR0UjE3M2ZaS2IwUlJzREZTU3NnMlJXbnBOVmozcVJy
```
This is Base64 encoded data.
### Step 4: Decode the Base64 data
```bash

bandit10@bandit:~$ base64 -d data.txt
```
Output:
```

The password is dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
```
The password is directly in the decoded text!

### Step 5: Log into Level 11
```bash

ssh bandit11@bandit.labs.overthewire.org -p 2220
```
Password: dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
