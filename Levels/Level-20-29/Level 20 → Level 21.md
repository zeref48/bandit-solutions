# 🔓 Level 20 → Level 21 — Connecting Programs with netcat

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit20` |
| **Password** | `0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO` (from Level 19) |

---

## 🎯 Challenge

> There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).
>
> **NOTE:** Try connecting to your own network daemon to see if it works as you think

**Commands you may need:** `ssh`, `nc`, `cat`, `bash`, `screen`, `tmux`, Unix 'job control' (`bg`, `fg`, `jobs`, `&`, `CTRL-Z`, …)

---

## 🧠 Understanding the Challenge

This level requires running **two programs simultaneously** that communicate over a network port.

### How it works

1. The setuid binary (`suconnect`) connects to a port you specify
2. It reads one line of text from that connection
3. It compares that line to the current level's password (`bandit20`)
4. If correct, it sends back the next level's password (`bandit21`)

### The Challenge

We need to:
1. Create a **server** that listens on a port and sends the bandit20 password
2. Run the **client** (`suconnect`) that connects to that port
3. The client will read the password, verify it, and return the next password

### Running Multiple Programs

Since we need both a server and a client running at the same time, we'll use:
- **Background processes** (`&`) - run a program in the background
- **Job control** (`fg`, `bg`, `jobs`, `Ctrl+Z`) - manage multiple processes
- Or use **two terminal windows** (not possible in a single SSH session)

---

## 💡 Solution

### Step 1: Connect to Level 20

```bash
ssh bandit20@bandit.labs.overthewire.org -p 2220# 
```
Password: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
### Step 2: Check what's in the home directory
```bash

bandit20@bandit:~$ ll
```
Output:
```

total 36
drwxr-xr-x   2 root     root      4096 Apr  3 15:17 ./
drwxr-xr-x 150 root     root      4096 Apr  3 15:20 ../
-rw-r--r--   1 root     root       220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root     root      3851 Apr  3 15:10 .bashrc
-rw-r--r--   1 root     root       807 Mar 31  2024 .profile
-rwsr-x---   1 bandit21 bandit20 15612 Apr  3 15:17 suconnect*
```
Notice the file suconnect with setuid bit set (owned by bandit21).
### Step 3: Create a background netcat server

We need to:

    Start a netcat server listening on a port

    Send the current password through that connection

    Run suconnect to connect to that port

```bash

bandit20@bandit:~$ echo "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" | nc -l -p 12345 &
```
Output:
```

[1] 19
```
Breakdown:

    echo "password" - outputs the password

    | - pipes it to netcat

    nc -l -p 12345 - listens on port 12345

    & - runs the command in the background (job number 1, PID 19)

### Step 4: Run the suconnect binary
```bash

bandit20@bandit:~$ ./suconnect 12345
```
Output:
```

Read: 0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO
Password matches, sending next password
EeoULMCra2q0dSkYj561DX7s1CpBuOBt
[1]+  Done                    echo "0qXahG8ZjOVMN9Ghs7iOWsCfZyXOUbYO" | nc -l -p 12345
```
The background job completes automatically after being used.

Step 5: Log into Level 21
```bash

ssh bandit21@bandit.labs.overthewire.org -p 2220
```
Password: EeoULMCra2q0dSkYj561DX7s1CpBuOBt
