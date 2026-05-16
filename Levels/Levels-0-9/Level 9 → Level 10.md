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
```
## 💡 Solution
### Step 1: Connect to Level 9
```bash

ssh bandit9@bandit.labs.overthewire.org -p 2220
```
Password: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
### Step 2: Check what files are in the home directory
```bash

bandit9@bandit:~$ ls -al
```
Output:
```

total 40
drwxr-xr-x   2 root     root     4096 Apr  3 15:17 .
drwxr-xr-x 150 root     root     4096 Apr  3 15:20 ..
-rw-r--r--   1 root     root      220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root     root     3851 Apr  3 15:10 .bashrc
-rw-r-----   1 bandit10 bandit9 19382 Apr  3 15:17 data.txt
-rw-r--r--   1 root     root      807 Mar 31  2024 .profile
```
There's a file named data.txt (about 19KB).
### Step 3: Extract readable strings and search for =
```bash

bandit9@bandit:~$ strings data.txt | grep '='
```
Output:
```

 ========== the
I\=Ow
V?L=
%3=VZ
========== password
={M\
========== is
=Dvq
=n/N
========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
zX]%=
]\{=
```
### Step 4: Identify the password

Looking at the output, we can see:

    ========== the

    ========== password

    ========== is

    ========== FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey

The password is clearly FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey - it follows the ========== and is the only long alphanumeric string.

### Step 5: Log into Level 10
```bash

ssh bandit10@bandit.labs.overthewire.org -p 2220
```
Password: FGUW5ilLVJrxX9kMYMmlN4MgbpfMiqey
