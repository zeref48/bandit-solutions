# 🔓 Level 1 → Level 2 — The Dashed Filename

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit1` |
| **Password** | `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If` (from Level 0) |

---

## 🎯 Challenge

> The password for the next level is stored in a file called **-** located in the home directory.

**Commands you may need:** `ls`, `cd`, `cat`, `file`, `du`, `find`

**Helpful Reading Material:**
- [Google Search for "dashed filename"](https://www.google.com/search?q=dashed+filename)
- [Advanced Bash-scripting Guide - Chapter 3 - Special Characters](https://tldp.org/LDP/abs/html/special-chars.html)

---

## 🧠 Understanding the Challenge

The challenge here is that the filename is just a **dash (`-`)** .

### Why is this tricky?

| Normal file | Problem with `-` |
|-------------|------------------|
| `cat filename` works fine | `cat -` doesn't work as expected |
| Commands interpret `-` as standard input/output | The shell thinks you want to read from stdin, not a file |

### What happens when you try `cat -`?

```bash
bandit1@bandit:~$ cat -
```
The terminal will just sit there, waiting for you to type input. This is because many Linux commands use - as a special character meaning "read from standard input" (your keyboard).

To exit this state, press Ctrl+C.
Why does this happen?

In Linux/Unix:

  - Most commands accept - as a shorthand for stdin/stdout

  - cat - means "read from keyboard and display it"

  - The shell doesn't know you meant "the actual file named -"

## 💡 Solution
### Step 1: Connect to Level 1
```bash

ssh bandit1@bandit.labs.overthewire.org -p 2220
```
Password: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
### Step 2: List files in the home directory
```bash

bandit1@bandit:~$ ls -al
```
Output:
```

total 24
-rw-r-----   1 bandit2 bandit1   33 Apr  3 15:17 -
drwxr-xr-x   2 root    root    4096 Apr  3 15:17 .
drwxr-xr-x 150 root    root    4096 Apr  3 15:20 ..
-rw-r--r--   1 root    root     220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root    root    3851 Apr  3 15:10 .bashrc
-rw-r--r--   1 root    root     807 Mar 31  2024 .profile
```
Notice the file named - (first line)!
### Step 3: Read the file named -

You cannot use:
```bash

bandit1@bandit:~$ cat -     # This will hang, waiting for keyboard input
```
Instead, use one of these methods:
- Method 1: Use ./ prefix (Easiest)
``` bash

bandit1@bandit:~$ cat ./-
```
Output:

```
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```
The ./ tells the shell: "Look in the current directory for a file named -"


- Method 2: Use absolute path (Works!)
```bash

bandit1@bandit:~$ cat /home/bandit1/-
```
Output:

```
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

### Step 4: Log into Level 2
```bash

ssh bandit2@bandit.labs.overthewire.org -p 2220
```
Password: 263JGJPfgU6LtdEvgfWU1XP5yac29mFx
