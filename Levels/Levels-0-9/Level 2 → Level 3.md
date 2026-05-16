# 🔓 Level 02 → Level 3 — Spaces in Filename

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit2` |
| **Password** | `263JGJPfgU6LtdEvgfWU1XP5yac29mFx` (from Level 1) |

---

## 🎯 Challenge

> The password for the next level is stored in a file called **spaces in this filename** located in the home directory.

**Commands you may need:** `ls`, `cd`, `cat`, `file`, `du`, `find`

---

## 🧠 Understanding the Challenge

The challenge here is that the filename contains **spaces**.

### Why is this tricky?

In Linux, spaces are used as **delimiters** between command arguments. When you type:

```bash
cat spaces in this filename
```
The shell interprets this as:

  - cat (command)

  - spaces (first argument - a file named "spaces")

  - in (second argument - a file named "in")

  - this (third argument - a file named "this")

  - filename (fourth argument - a file named "filename")

It thinks you're trying to cat four separate files — not one file with spaces in its name.

## 💡 Solution
### Step 1: Connect to Level 2
```bash

ssh bandit2@bandit.labs.overthewire.org -p 2220
```
Password: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx
### Step 2: List files in the home directory
```bash

bandit2@bandit:~$ ls -al
```
Output:

```
total 24
drwxr-xr-x   2 root    root    4096 Apr  3 15:17 .
drwxr-xr-x 150 root    root    4096 Apr  3 15:20 ..
-rw-r--r--   1 root    root     220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root    root    3851 Apr  3 15:10 .bashrc
-rw-r--r--   1 root    root     807 Mar 31  2024 .profile
-rw-r-----   1 bandit3 bandit2   33 Apr  3 15:17 --spaces in this filename--
```
Notice the file named --spaces in this filename-- !!!
### Step 3: Try to read the file (and see what doesn't work)
```bash

bandit2@bandit:~$ cat "--spaces in this filename--"
```
Output:
```

cat: unrecognized option '--spaces in this filename--'
Try 'cat --help' for more information.
```
This fails because cat sees --spaces and thinks it's an option flag.
### Step 4: The correct way to read the file

Use ./ prefix to tell the shell it's a file in the current directory:
```bash

bandit2@bandit:~$ cat ./--spaces\ in\ this\ filename--
```
Or using quotes with ./:
```bash

bandit2@bandit:~$ cat "./--spaces in this filename--"
```
Output:
text

MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx


### Step 5: Log into Level 3
```bash

ssh bandit3@bandit.labs.overthewire.org -p 2220
```
Password: MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
