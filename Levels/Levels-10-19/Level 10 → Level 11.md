
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
