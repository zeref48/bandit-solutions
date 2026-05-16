# 🔓 Level 6 → Level 7 — Finding Files by Owner and Group

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit6` |
| **Password** | `HWasnPhtq9AVKe0dmk45nxy20cvUa6EG` (from Level 5) |

---

## 🎯 Challenge

> The password for the next level is stored somewhere on the server and has all of the following properties:
> - owned by user **bandit7**
> - owned by group **bandit6**
> - **33 bytes** in size

**Commands you may need:** `ls`, `cd`, `cat`, `file`, `du`, `find`, `grep`

---

## 🧠 Understanding the Challenge

This level requires searching the **entire filesystem** for a file with specific ownership and size properties.

### The `find` Command with User/Group Filters

| Criteria | Purpose | Example |
|----------|---------|---------|
| `-user bandit7` | Find files owned by user bandit7 | `find / -user bandit7` |
| `-group bandit6` | Find files owned by group bandit6 | `find / -group bandit6` |
| `-size 33c` | Find files exactly 33 bytes | `find / -size 33c` |
| `-type f` | Find only regular files | `find / -type f` |

### Why search from root (`/`)?

The file could be **anywhere** on the server:
- In `/home/` directories
- In `/var/` directories
- In `/tmp/` directories
- In system directories like `/etc/` or `/usr/`

Starting from `/` (root) searches the entire filesystem.

### Handling Permission Denied Errors

When searching the entire filesystem, you'll get many "Permission denied" errors. You can:
1. Ignore them (they don't affect results)
2. Redirect errors to `/dev/null` to hide them

```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```
## 💡 Solution
### Step 1: Connect to Level 6
```bash

ssh bandit6@bandit.labs.overthewire.org -p 2220
```
Password: HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
### Step 2: Search the entire filesystem

We need to find a file that is:

  - Owned by user bandit7 (-user bandit7)

  - Owned by group bandit6 (-group bandit6)

  - Exactly 33 bytes in size (-size 33c)

  - A regular file (-type f)

The complete find command:
```bash

bandit6@bandit:~$ find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```
Breakdown of the command:
```bash

find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
│     │      │    │          │           │        │
│     │      │    │          │           │        └── hide errors
│     │      │    │          │           └── exactly 33 bytes
│     │      │    │          └── owned by group bandit6
│     │      │    └── owned by user bandit7
│     │      └── only regular files
│     └── start searching from root (entire system)
└── find command
```
### Step 3: Find the file

Output:
```

/var/lib/dpkg/info/bandit7.password
```
This is the path to the file containing the password.
### Step 4: Read the file
```bash

bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
```
Output:
```

morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
```

### Step 5: Log into Level 7
```bash

ssh bandit7@bandit.labs.overthewire.org -p 2220
```
Password: morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
