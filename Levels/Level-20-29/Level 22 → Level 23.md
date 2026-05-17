# 🔓 Level 22 → Level 23 — Cron Jobs and Script Analysis

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit22` |
| **Password** | `tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q` (from Level 21) |

---

## 🎯 Challenge

> A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.
>
> **NOTE:** Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

**Commands you may need:** `cron`, `crontab`, `crontab(5)` (use "man 5 crontab" to access this)

---

## 🧠 Understanding the Challenge

This level builds on the previous cron job concept, but requires analyzing a shell script that creates temporary files.

### The Approach

1. Find the cron job for bandit23 in `/etc/cron.d/`
2. Examine the script it runs
3. Understand what the script does
4. Find where the script writes the password or output

### Script Analysis Skills

When analyzing unknown scripts, look for:
- Where files are created or written to
- What commands are executed
- Where output is redirected
- Variable values and expansions

---

## 💡 Solution

### Step 1: Connect to Level 22

```bash
ssh bandit22@bandit.labs.overthewire.org -p 2220
```
Password: tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
### Step 2: Look in the cron.d directory
```bash

bandit22@bandit:~$ ll /etc/cron.d/
```
Output:
```

total 60
drwxr-xr-x   2 root root  4096 Apr  3 15:20 ./
drwxr-xr-x 128 root root 12288 May 10 08:58 ../
-r--r-----   1 root root    47 Apr  3 15:18 behemoth4_cleanup
-rw-r--r--   1 root root   123 Apr  3 15:10 clean_tmp
-rw-r--r--   1 root root   120 Apr  3 15:17 cronjob_bandit22
-rw-r--r--   1 root root   122 Apr  3 15:17 cronjob_bandit23
-rw-r--r--   1 root root   120 Apr  3 15:17 cronjob_bandit24
-rw-r--r--   1 root root   201 Apr  8  2024 e2scrub_all
-r--r-----   1 root root    48 Apr  3 15:19 leviathan5_cleanup
-rw-------   1 root root   138 Apr  3 15:19 manpage3_resetpw_job
-rwx------   1 root root    52 Apr  3 15:20 otw-tmp-dir*
-rw-r--r--   1 root root   102 Mar 31  2024 .placeholder
-rw-r--r--   1 root root   396 Jan  9  2024 sysstat
```
There's a file named cronjob_bandit23.
### Step 3: View the cron job file
``` bash

bandit22@bandit:~$ cat /etc/cron.d/cronjob_bandit23
```
Output:
```

@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
```
This shows:

    @reboot - runs once when the system boots

    * * * * * - runs every minute

    User: bandit23

    Command: /usr/bin/cronjob_bandit23.sh

    Output redirected to /dev/null (discarded)

### Step 4: Examine the script
```bash

bandit22@bandit:~$ cat /usr/bin/cronjob_bandit23.sh
```
Output:
```

#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```
### Step 5: Understand what the script does

Let's break down the script:
```bash

# Get the current username
myname=$(whoami)

# Create a target filename by:
# 1. Echoing "I am user $myname"
# 2. Taking MD5 hash of that string
# 3. Cutting only the hash (first field)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

# Copy the password to /tmp/$mytarget
cat /etc/bandit_pass/$myname > /tmp/$mytarget
```
The script:

    Takes the current username (bandit23 when run by cron)

    Creates an MD5 hash of the string "I am user bandit23"

    Uses that hash as a filename in /tmp/

    Writes the password to that file

### Step 6: Try the wrong approach first (common mistake)
```bash

bandit22@bandit:~$ echo "bandit23" | md5sum | cut -d ' ' -f 1
```
Output:
```

35964510399388ff8cd7da6f7927c82b
```
```bash

bandit22@bandit:~$ cat /tmp/35964510399388ff8cd7da6f7927c82b
cat: /tmp/35964510399388ff8cd7da6f7927c82b: No such file or directory
```
This doesn't work because the script uses the exact phrase "I am user bandit23", not just "bandit23".
### Step 7: Calculate the correct MD5 hash for bandit23
```bash

bandit22@bandit:~$ echo "I am user bandit23" | md5sum | cut -d ' ' -f 1
```
Output:
```

8ca319486bfbbc3663ea0fbe81326349
```
This is the correct filename where the password is stored.
### Step 8: Read the password file
```bash

bandit22@bandit:~$ cat /tmp/8ca319486bfbbc3663ea0fbe81326349
```
Output:
```

0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
```

### Step 9: Log into Level 23
```bash

ssh bandit23@bandit.labs.overthewire.org -p 2220
```
Password: 0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
