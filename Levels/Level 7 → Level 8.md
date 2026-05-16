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
```
## 💡 Solution
### Step 1: Connect to Level 7
```bash

ssh bandit7@bandit.labs.overthewire.org -p 2220
```
Password: morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
### Step 2: Check what files are in the home directory
```bash

bandit7@bandit:~$ ls -la
```
Output:
```

total 4108
drwxr-xr-x   2 root    root       4096 Apr  3 15:18 .
drwxr-xr-x 150 root    root       4096 Apr  3 15:20 ..
-rw-r--r--   1 root    root        220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root    root       3851 Apr  3 15:10 .bashrc
-rw-r-----   1 bandit8 bandit7 4184396 Apr  3 15:18 data.txt
-rw-r--r--   1 root    root        807 Mar 31  2024 .profile
```
There's a file named data.txt (about 4.1MB in size).
### Step 3: Search for "millionth" in data.txt
```bash

bandit7@bandit:~$ grep millionth data.txt
```
Output:
```

millionth       dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```
The password is the text after "millionth" (separated by a tab).
### Step 4: Extract just the password (optional)

If you want only the password without the word "millionth":
```bash

bandit7@bandit:~$ grep millionth data.txt | awk '{print $2}'
```
Output:
```

dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
```
Or using cut:
```bash

bandit7@bandit:~$ grep millionth data.txt | cut -f2
```

### Step 5: Log into Level 8
```bash

ssh bandit8@bandit.labs.overthewire.org -p 2220
```
Password: dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
