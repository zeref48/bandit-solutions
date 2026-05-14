# 🔓 Level 5 → Level 6 — Finding Files by Properties

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit5` |
| **Password** | `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw` (from Level 4) |

---

## 🎯 Challenge

> The password for the next level is stored in a file somewhere under the **inhere** directory and has all of the following properties:
> - human-readable
> - 1033 bytes in size
> - not executable

**Commands you may need:** `ls`, `cd`, `cat`, `file`, `du`, `find`

---

## 🧠 Understanding the Challenge

This level introduces the powerful `find` command with multiple search criteria.

### The `find` Command

The `find` command searches for files and directories based on various properties:

```bash
find [path] [criteria] [action]
```
## 💡 Solution
### Step 1: Connect to Level 5
```bash

ssh bandit5@bandit.labs.overthewire.org -p 2220
```
Password: 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
### Step 2: Check what's in the home directory
```bash

bandit5@bandit:~$ ls
```
Output:
```

inhere
```
### Step 3: Go into the inhere directory and list contents
```bash

bandit5@bandit:~$ cd inhere/
bandit5@bandit:~/inhere$ ls
```
Output:
```

maybehere00  maybehere02  maybehere04  maybehere06  maybehere08  maybehere10  maybehere12  maybehere14  maybehere16  maybehere18
maybehere01  maybehere03  maybehere05  maybehere07  maybehere09  maybehere11  maybehere13  maybehere15  maybehere17  maybehere19
```
There are 20 subdirectories (maybehere00 through maybehere19), each containing various files.
### Step 4: Use find to locate the file with all properties

We need a file that is:

    - Human-readable (-exec file {} \; or combine with -readable)

    - Exactly 1033 bytes (-size 1033c)

    - Not executable (! -executable or -not -executable)

The complete find command:
```bash

bandit5@bandit:~/inhere$ find . -type f -size 1033c ! -executable -exec file {} \;
```
Breakdown of the command:
```bash

find . -type f -size 1033c ! -executable -exec file {} \;
│     │      │         │            │            │
│     │      │         │            │            └── run file command
│     │      │         │            └── NOT executable
│     │      │         └── exactly 1033 bytes
│     │      └── only files (not directories)
│     └── start from current directory
└── find command
```
### Step 5: Identify the correct file

Output:
```

./maybehere07/.file2: ASCII text, with very long lines (1000)
```
This shows that ./maybehere07/.file2 is an ASCII text file (human-readable) of the right size. The (1000) indicates very long lines, not the file size.
### Step 6: Read the file
```bash

bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
```
Output:
```

HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```


### Step 7: Log into Level 6
```bash

ssh bandit6@bandit.labs.overthewire.org -p 2220
```
Password: HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
