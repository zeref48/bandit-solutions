# 🔓 Level 11 → Level 12 — ROT13 Cipher

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit11` |
| **Password** | `dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr` (from Level 10) |

---

## 🎯 Challenge

> The password for the next level is stored in the file **data.txt**, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

**Commands you may need:** `grep`, `sort`, `uniq`, `strings`, `base64`, `tr`, `tar`, `gzip`, `bzip2`, `xxd`

**Helpful Reading Material:**
- [Rot13 on Wikipedia](https://en.wikipedia.org/wiki/ROT13)

---

## 🧠 Understanding the Challenge

This level introduces the **ROT13 cipher** and the `tr` command to translate characters.

### What is ROT13?

ROT13 (rotate by 13 places) is a simple letter substitution cipher that replaces a letter with the 13th letter after it in the alphabet.

| Letter | ROT13 | Letter | ROT13 |
|--------|-------|--------|-------|
| A → N | a → n | N → A | n → a |
| B → O | b → o | O → B | o → b |
| C → P | c → p | P → C | p → c |
| ... | ... | ... | ... |
| M → Z | m → z | Z → M | z → m |

### ROT13 Properties

- It's its own inverse: applying ROT13 twice returns the original text
- Only letters A-Z and a-z are affected; numbers and punctuation stay the same
- Used to obscure text (not for real encryption)

### The `tr` Command

`tr` (translate) replaces or deletes characters:

```bash
tr [options] set1 set2
