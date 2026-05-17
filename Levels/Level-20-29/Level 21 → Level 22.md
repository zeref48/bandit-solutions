# 🔓 Level 21 → Level 22 — Cron Jobs

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit21` |
| **Password** | `EeoULMCra2q0dSkYj561DX7s1CpBuOBt` (from Level 20) |

---

## 🎯 Challenge

> A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.

**Commands you may need:** `cron`, `crontab`, `crontab(5)` (use "man 5 crontab" to access this)

---

## 🧠 Understanding the Challenge

This level introduces **cron**, the time-based job scheduler in Linux.

### What is Cron?

Cron is a daemon that executes scheduled commands at specific times or intervals. It's used for:
- Automated backups
- System maintenance tasks
- Running scripts periodically

### Cron Configuration Locations

| Location | Purpose |
|----------|---------|
| `/etc/crontab` | System-wide crontab file |
| `/etc/cron.d/` | Directory for individual cron job files |
| `/etc/cron.hourly/` | Scripts run every hour |
| `/etc/cron.daily/` | Scripts run every day |
| `/etc/cron.weekly/` | Scripts run every week |
| `/etc/cron.monthly/` | Scripts run every month |
| `crontab -e` | User-specific crontab (editable) |

## 💡 Solution

### Step 1: Connect to Level 21

```bash
ssh bandit21@bandit.labs.overthewire.org -p 2220
```
Password: EeoULMCra2q0dSkYj561DX7s1CpBuOBt
### Step 2: Check home directory contents (optional)
```bash

bandit21@bandit:~$ ll
```
Output:
```

total 24
drwxr-xr-x   2 root     root     4096 Apr  3 15:17 ./
drwxr-xr-x 150 root     root     4096 Apr  3 15:20 ../
-rw-r--r--   1 root     root      220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root     root     3851 Apr  3 15:10 .bashrc
-r--------   1 bandit21 bandit21   33 Apr  3 15:17 .prevpass
-rw-r--r--   1 root     root      807 Mar 31  2024 .profile
```
### Step 3: Look in the cron.d directory
```bash

bandit21@bandit:~$ ls -al /etc/cron.d/
```
Output:
```

total 60
drwxr-xr-x   2 root root  4096 Apr  3 15:20 .
drwxr-xr-x 128 root root 12288 May 10 08:58 ..
-r--r-----   1 root root    47 Apr  3 15:18 behemoth4_cleanup
-rw-r--r--   1 root root   123 Apr  3 15:10 clean_tmp
-rw-r--r--   1 root root   120 Apr  3 15:17 cronjob_bandit22
-rw-r--r--   1 root root   122 Apr  3 15:17 cronjob_bandit23
-rw-r--r--   1 root root   120 Apr  3 15:17 cronjob_bandit24
-rw-r--r--   1 root root   201 Apr  8  2024 e2scrub_all
-r--r-----   1 root root    48 Apr  3 15:19 leviathan5_cleanup
-rw-------   1 root root   138 Apr  3 15:19 manpage3_resetpw_job
-rwx------   1 root root    52 Apr  3 15:20 otw-tmp-dir
-rw-r--r--   1 root root   102 Mar 31  2024 .placeholder
-rw-r--r--   1 root root   396 Jan  9  2024 sysstat
```
There's a file named cronjob_bandit22.
### Step 4: View the cron job file
```bash

bandit21@bandit:~$ cat /etc/cron.d/cronjob_bandit22
```
Output:
```

@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```
This shows:

    @reboot - runs once when the system boots

    * * * * * - runs every minute

    User: bandit22

    Command: /usr/bin/cronjob_bandit22.sh

    Output redirected to /dev/null (discarded)

### Step 5: Look at the script being executed
```bash

bandit21@bandit:~$ cat /usr/bin/cronjob_bandit22.sh
```
Output:
```

#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```
This script:

    Sets permissions on a file in /tmp/

    Writes the bandit22 password to that file

### Step 6: Check the file in /tmp
```bash

bandit21@bandit:~$ ls -al /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```
Output:
```

-rw-r--r-- 1 bandit22 bandit22 33 May 17 18:34 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```
The file exists and is world-readable (-rw-r--r--).
### Step 7: Read the file containing the password
```bash

bandit21@bandit:~$ cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```
Output:
```

tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
```

Step 8: Log into Level 22
```bash

ssh bandit22@bandit.labs.overthewire.org -p 2220
```
Password: tRae0UfB9v0UzbCdn9cY0gQnds9GF58Q
