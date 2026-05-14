# 🔓 Level 3 → Level 4 — Hidden Files

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit3` |
| **Password** | `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx` (from Level 2) |

---

## 🎯 Challenge

> The password for the next level is stored in a hidden file in the **inhere** directory.

**Commands you may need:** `ls`, `cd`, `cat`, `file`, `du`, `find`

---

## 🧠 Understanding the Challenge

In Linux, **hidden files** are files that start with a dot (`.`). 

### What are hidden files?

| File | Hidden? | How to see |
|------|---------|------------|
| `readme` | No (visible) | `ls` |
| `.hidden` | Yes (hidden) | `ls -la` or `ls -a` |
| `.bashrc` | Yes (hidden) | `ls -la` |
| `..` | Special (parent directory) | `ls -la` |
| `.` | Special (current directory) | `ls -la` |

### How to see hidden files

| Command | Shows |
|---------|-------|
| `ls` | Only non-hidden files |
| `ls -a` | All files (including hidden, `.`, and `..`) |
| `ls -la` | All files with detailed information (permissions, size, etc.) |

### The `-a` flag

`-a` stands for **"all"** — it shows everything, including hidden files.


---

## 💡 Solution

### Step 1: Connect to Level 3

```bash
ssh bandit3@bandit.labs.overthewire.org -p 2220
```
Password: MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
### Step 2: Check what's in the home directory

First, see what files are visible:
```bash

bandit3@bandit:~$ ls -al
```
Output:
```

total 24
drwxr-xr-x   3 root root 4096 Apr  3 15:18 .
drwxr-xr-x 150 root root 4096 Apr  3 15:20 ..
-rw-r--r--   1 root root  220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root root 3851 Apr  3 15:10 .bashrc
drwxr-xr-x   2 root root 4096 Apr  3 15:18 inhere
-rw-r--r--   1 root root  807 Mar 31  2024 .profile
```
There's a directory named inhere.
### Step 3: Go into the inhere directory
```bash

bandit3@bandit:~$ cd inhere/
```
### Step 4: List all files in inhere (including hidden)
```bash

bandit3@bandit:~/inhere$ ls -al
```
Output:
```

total 12
drwxr-xr-x 2 root    root    4096 Apr  3 15:18 .
drwxr-xr-x 3 root    root    4096 Apr  3 15:18 ..
-rw-r----- 1 bandit4 bandit3   33 Apr  3 15:18 ...Hiding-From-You
```
Notice the file named ...Hiding-From-You — it starts with three dots, so it's hidden!

    💡 Why three dots? Any file starting with a dot (.) is hidden. ...Hiding-From-You starts with a dot, so it's hidden. The number of dots doesn't matter — one dot or three dots, still hidden!

### Step 5: Read the hidden file
```bash

bandit3@bandit:~/inhere$ cat ...Hiding-From-You
```
Output:
```

2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```


### Step 6: Log into Level 4
```bash

ssh bandit4@bandit.labs.overthewire.org -p 2220
```
Password: 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ


