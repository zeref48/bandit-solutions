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
ssh bandit20@bandit.labs.overthewire.org -p 2220# 🔓 Level 20 → Level 21 — Connecting Programs with netcat

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
ssh bandit20@bandit.labs.overthewire.org -p 2220
