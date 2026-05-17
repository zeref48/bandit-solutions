# 🔓 Level 19 → Level 20 — Using setuid Binaries

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit19` |
| **Password** | `cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8` (from Level 18) |

---

## 🎯 Challenge

> To gain access to the next level, you should use the **setuid binary** in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

**Helpful Reading Material:**
- [setuid on Wikipedia](https://en.wikipedia.org/wiki/Setuid)

---

## 🧠 Understanding the Challenge

This level introduces the concept of **setuid binaries** (Set User ID).

### What is setuid?

setuid is a special permission that allows a program to run with the privileges of the **file owner**, not the user who executes it.

| Normal Program | setuid Program |
|----------------|----------------|
| Runs as the user who executes it | Runs as the file owner |
| Can only access what the user can access | Can access what the owner can access |
| Example: `ls` runs as you | Example: `passwd` runs as root |

### Viewing setuid permissions

```bash
ls -l filename
```
## 💡 Solution
### Step 1: Connect to Level 19
```bash

ssh bandit19@bandit.labs.overthewire.org -p 2220
```
Password: cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
### Step 2: Check what's in the home directory
```bash

bandit19@bandit:~$ ll
```
Output:
```

total 36
drwxr-xr-x   2 root     root      4096 Apr  3 15:17 ./
drwxr-xr-x 150 root     root      4096 Apr  3 15:20 ../
-rwsr-x---   1 bandit20 bandit19 14888 Apr  3 15:17 bandit20-do*
-rw-r--r--   1 root     root       220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root     root      3851 Apr  3 15:10 .bashrc
-rw-r--r--   1 root     root       807 Mar 31  2024 .profile
```
Notice the file bandit20-do with permissions -rwsr-x---:

    The s in the owner execute position means setuid is set

    Owner is bandit20, so it runs with bandit20's privileges

    Group is bandit19, so only bandit19 (you) can execute it

### Step 3: Check the password file permissions
```bash

bandit19@bandit:~$ ls -l /etc/bandit_pass/bandit20
```
Output:
```

-r-------- 1 bandit20 bandit20 33 Apr  3 15:17 /etc/bandit_pass/bandit20
```
Only bandit20 can read this file.
### Step 4: Execute the binary without arguments
```bash

bandit19@bandit:~$ ./bandit20-do
```
Output:
```

Run a command as another user.
  Example: ./bandit20-do whoami
```
This tells us the binary runs a command as another user (bandit20).
### Step 5: Test who you are when using the binary
```bash

bandit19@bandit:~$ ./bandit20-do whoami
```
Output:
```

bandit20
```
This confirms the binary runs commands as bandit20.
### Step 6: Use the binary to read the password file
```bash

bandit19@bandit:~$ ./bandit20-do cat /etc/bandit_pass/bandit20
```
Output:
```

0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO

```
### Step 7: Log into Level 20
```bash

ssh bandit20@bandit.labs.overthewire.org -p 2220
```
Password: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
