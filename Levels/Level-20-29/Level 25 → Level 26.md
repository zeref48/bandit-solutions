# 🔓 Level 25 → Level 26 — Breaking Out of a Restricted Shell

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit25` |
| **Password** | `gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8` (from Level 24) |

---

## 🎯 Challenge

> Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not **/bin/bash**, but something else. Find out what it is, how it works and how to break out of it.
>
> **NOTE:** if you're a Windows user and typically use Powershell to ssh into bandit: Powershell is known to cause issues with the intended solution to this level. You should use command prompt instead.

**Commands you may need:** `ssh`, `cat`, `more`, `vi`, `ls`, `id`, `pwd`

---

## 🧠 Understanding the Challenge

This level involves breaking out of a restricted shell environment.

### Key Concepts

| Concept | Explanation |
|---------|-------------|
| **Default shell** | The program that runs when you log in (e.g., /bin/bash) |
| **Restricted shell** | A shell with limited capabilities |
| **/etc/passwd** | File that contains user account information including default shell |
| **more command** | Pager program that can execute commands from within |
| **vi/vim editor** | Can be used to spawn a shell |

### The Goal

1. Find out what shell bandit26 uses
2. Log in as bandit26 (using the SSH key from bandit25)
3. Break out of the restricted shell to get a normal shell
4. Read the password for bandit26

---

## 💡 Solution

### Step 1: Connect to Level 25

```bash
ssh bandit25@bandit.labs.overthewire.org -p 2220
