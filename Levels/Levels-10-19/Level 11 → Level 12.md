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
```
## 💡 Solution
### Step 1: Connect to Level 11
```bash

ssh bandit11@bandit.labs.overthewire.org -p 2220
```
Password: dtR173fZKb0RRsDFSGsg2RWnpNVj3qRr
### Step 2: Check what files are in the home directory
```bash

bandit11@bandit:~$ ls -al
```
Output:
```
total 24
drwxr-xr-x   2 root     root     4096 Apr  3 15:17 .
drwxr-xr-x 150 root     root     4096 Apr  3 15:20 ..
-rw-r--r--   1 root     root      220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root     root     3851 Apr  3 15:10 .bashrc
-rw-r-----   1 bandit12 bandit11   49 Apr  3 15:17 data.txt
-rw-r--r--   1 root     root      807 Mar 31  2024 .profile
```
There's a file named data.txt.
### Step 3: View the encoded data
```bash

bandit11@bandit:~$ cat data.txt
```
Output:
```

Gur cnffjbeq vf 7k16JArUVv5LxVuJfsSVdbbtaHGlw9D4
```
This is ROT13 encoded text.
### Step 4: Decode ROT13 using tr

ROT13 maps:

    A-Z → N-ZA-M (first 13 letters to last 13, and vice versa)

    a-z → n-za-m

Using tr:
```bash

bandit11@bandit:~$ cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```
Output:
```

The password is 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
```
Note: Be careful with the pipe syntax — only one | is needed, not two!


### Step 7: Log into Level 12
```bash

ssh bandit12@bandit.labs.overthewire.org -p 2220
```
Password: 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
