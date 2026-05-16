# 🔓 Level 13 → Level 14 — Using SSH Private Keys

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit13` |
| **Password** | `FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn` (from Level 12) |

---

## 🎯 Challenge

> The password for the next level is stored in **/etc/bandit_pass/bandit14** and can only be read by user bandit14. For this level, you don't get the next password, but you get a private SSH key that can be used to log into the next level.

**Commands you may need:** `ssh`, `scp`, `chmod`, `cat`

---

## 🧠 Understanding the Challenge

This level introduces **SSH key authentication** as an alternative to password authentication.

### The Problem with Localhost

The Bandit server blocks SSH connections from `localhost` (the same server) to conserve resources. Therefore, you cannot use the key while logged into bandit13. You must:

1. Copy the private key to your **local machine**
2. Use it from there to connect directly to bandit14

### SSH Key Authentication

Instead of using a password, you can use a **key pair**:
- **Private key** (keep secret, permissions 600)
- **Public key** (placed on the server)

### Using an SSH Key from Your Local Machine

```bash
ssh -i private_key_file username@host -p port
```
## 💡 Solution
### Step 1: On your local machine, copy the private key from bandit13

Open a new terminal on your computer (not connected to the Bandit server):
```bash

scp -P 2220 bandit13@bandit.labs.overthewire.org:sshkey.private ~/sshkey.private
```
Password: FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn

What this does:

    scp = secure copy (transfers files over SSH)

    -P 2220 = port 2220 (note: uppercase P for scp)

    bandit13@...:sshkey.private = source file on the server

    ~/sshkey.private = destination on your local machine

### Step 2: Set correct permissions on the private key
```bash

chmod 600 ~/sshkey.private
```
SSH requires private keys to have permissions 600 (only owner can read/write).
### Step 3: Use the key to connect directly to bandit14
```bash

ssh -i ~/sshkey.private bandit14@bandit.labs.overthewire.org -p 2220
```
Note: No password needed! The key authenticates you.
### Step 4: Once logged in as bandit14, read the password
```bash

bandit14@bandit:~$ cat /etc/bandit_pass/bandit14
```
Output:
```

MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
```

### Step 5: Log into Level 14 normally (optional)
```bash

ssh bandit14@bandit.labs.overthewire.org -p 2220
```
Password: MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS
