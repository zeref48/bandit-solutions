# 🔓 Level 18 → Level 19 — Escaping a Restricted Shell

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit18` |
| **Password** | `x2gLTTjFwMOhQ8oWNbMN362QKxfRqGlO` (from Level 17) |

---

## 🎯 Challenge

> The password for the next level is stored in a file **readme** in the homedirectory. Unfortunately, someone has modified **.bashrc** to log you out when you log in with SSH.

**Commands you may need:** `ssh`, `ls`, `cat`

---

## 🧠 Understanding the Challenge

This level demonstrates how to bypass a restricted shell that logs you out immediately.

### The Problem

When you try to log in normally:

```bash
ssh bandit18@bandit.labs.overthewire.org -p 2220
```
## 💡 Solution
### Step 1: Try normal login (to see the problem)
```bash

ssh bandit18@bandit.labs.overthewire.org -p 2220
```
Output:
```

[Welcome banner...]
Byebye !
Connection to bandit.labs.overthewire.org closed.
```
### Step 2: Execute a command directly over SSH

Instead of logging in interactively, run a command. First, list files:
```bash

ssh bandit18@bandit.labs.overthewire.org -p 2220 "ls"
```
Output:
```

readme
```
This shows there's a readme file in the home directory.
### Step 3: Read the readme file
```bash

ssh bandit18@bandit.labs.overthewire.org -p 2220 "cat ~/readme"
```
Output:
text

cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8

### Step 4: Save the password
```bash

echo "bandit19: cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8" >> ~/bandit_notes.txt
```
### Step 5: Log into Level 19
```bash

ssh bandit19@bandit.labs.overthewire.org -p 2220
```
Password: cGWpMaKXVwDUNgPAVJbWYuGHVn9zl3j8
