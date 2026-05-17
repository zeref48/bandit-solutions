# 🔓 Level 17 → Level 18 — Comparing Files with diff

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit17` |
| **Password** | Use the SSH private key from Level 16 |

**Credentials:** `ssh -i bandit17_key bandit17@bandit.labs.overthewire.org -p 2220`

---

## 🎯 Challenge

> There are 2 files in the homedirectory: **passwords.old** and **passwords.new**. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new
>
> **NOTE:** if you have solved this level and see 'Byebye!' when trying to log into bandit18, this is related to the next level, bandit19

**Commands you may need:** `cat`, `grep`, `ls`, `diff`

---

## 🧠 Understanding the Challenge

This level introduces the `diff` command, which compares files line by line and shows the differences.

### The `diff` Command

`diff` compares files and displays the lines that differ:

```bash
diff file1 file2
```
## 💡 Solution
### Step 1: Connect to Level 17 using the SSH key
```bash

ssh -i ~/bandit17_key bandit17@bandit.labs.overthewire.org -p 2220
```
Step 2: Check what files are in the home directory
```bash

bandit17@bandit:~$ ll
```
Output:
```

total 36
drwxr-xr-x   3 root     root     4096 Apr  3 15:17 ./
drwxr-xr-x 150 root     root     4096 Apr  3 15:20 ../
-rw-r-----   1 bandit17 bandit17   33 Apr  3 15:17 .bandit16.password
-rw-r--r--   1 root     root      220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root     root     3851 Apr  3 15:10 .bashrc
-rw-r-----   1 bandit18 bandit17 3300 Apr  3 15:17 passwords.new
-rw-r-----   1 bandit18 bandit17 3300 Apr  3 15:17 passwords.old
-rw-r--r--   1 root     root      807 Mar 31  2024 .profile
drwxr-xr-x   2 root     root     4096 Apr  3 15:17 .ssh/
```
There are two files: passwords.old and passwords.new.
### Step 3: Preview the files (optional)
```bash

bandit17@bandit:~$ head passwords.old
l48kFEV9T4L7QR4n7aSxxiS7tWKNlM03
YowiCeTsti6dcSmrzZjBKOFo5YYd3BOH
vzxzxTYHBIKaf00rQKawPrRk0F669IeO
sD3RMavhe5MupXYdEnGMrY9Qj49fRjLz
87ZGorjf6jTBOx7lsa0AygxTdXoVWAdQ
s5YoafbakHEl5wEF2aTpOBVv2VV7xbA3
NeEvNv8Ga9bUQDRIXXnae4o9EN9nXQfh
PeoMKhyuWTOOn2wwCS7nFD7sgJfMOQfZ
m7KwZnaad6e02WyxlrBSDxPfGIpElUZa
fOhRzt0lOcobOKvXVmav2dXXOBiiVK12

bandit17@bandit:~$ head passwords.new
l48kFEV9T4L7QR4n7aSxxiS7tWKNlM03
YowiCeTsti6dcSmrzZjBKOFo5YYd3BOH
vzxzxTYHBIKaf00rQKawPrRk0F669IeO
sD3RMavhe5MupXYdEnGMrY9Qj49fRjLz
87ZGorjf6jTBOx7lsa0AygxTdXoVWAdQ
s5YoafbakHEl5wEF2aTpOBVv2VV7xbA3
NeEvNv8Ga9bUQDRIXXnae4o9EN9nXQfh
PeoMKhyuWTOOn2wwCS7nFD7sgJfMOQfZ
m7KwZnaad6e02WyxlrBSDxPfGIpElUZa
fOhRzt0lOcobOKvXVmav2dXXOBiiVK12
```
Notice the first 10 lines are identical in both files. The difference is further down.
### Step 4: Compare the files using diff
```bash

bandit17@bandit:~$ diff passwords.old passwords.new
```
Output:
```

42c42
< KxOU4IzbXM8j8HeAWPAXTd1eC77mp1qV
---
> x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO
```
This shows:

    Line 42 in passwords.old is < KxOU4IzbXM8j8HeAWPAXTd1eC77mp1qV

    Line 42 in passwords.new is > x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO

### Step 5: Extract the password

The password for Level 18 is the line from passwords.new:
text

x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO



Step 6: Log into Level 18
```bash

ssh bandit18@bandit.labs.overthewire.org -p 2220
```
Password: x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO

    ⚠️ Note: If you see "Byebye!" when trying to log in, don't worry! That's part of Level 18's challenge. You'll need to handle that in the next level.
