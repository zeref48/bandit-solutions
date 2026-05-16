# 🔓 Level 4 → Level 5 — Finding Human-Readable Files

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit4` |
| **Password** | `2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ` (from Level 3) |

---

## 🎯 Challenge

> The password for the next level is stored in the only human-readable file in the **inhere** directory. Tip: if your terminal is messed up, try the "reset" command.

**Commands you may need:** `ls`, `cd`, `cat`, `file`, `du`, `find`

---

## 🧠 Understanding the Challenge

This level introduces the concept of **file types** and **human-readable** content.

### What makes a file "human-readable"?

| File Type | Human-Readable? | Example |
|-----------|-----------------|---------|
| Text files | ✅ Yes | `Hello world`, `password123` |
| Source code | ✅ Yes | `#include <stdio.h>` |
| Configuration files | ✅ Yes | `username=admin` |
| Binary executables | ❌ No | `ELF` header, random bytes |
| DOS executables | ❌ No | `MZ` header, machine code |
| Images | ❌ No | PNG/JPG headers, binary data |
| Compiled programs | ❌ No | Machine code |

### The `file` Command

The `file` command identifies what type of file something is:

```bash
file filename
```
## 💡 Solution
### Step 1: Connect to Level 4
```bash

ssh bandit4@bandit.labs.overthewire.org -p 2220
```
Password: 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
### Step 2: Check what's in the home directory
```bash

bandit4@bandit:~$ ls
```
Output:
```

inhere
```
### Step 3: Go into the inhere directory
```bash

bandit4@bandit:~$ cd inhere/
```
### Step 4: List all files
```bash

bandit4@bandit:~/inhere$ ls
```
Output:
```

-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
```
There are 10 files named -file00 through -file09.
### Step 5: Identify file types using find with file
```bash

bandit4@bandit:~/inhere$ find . -type f -exec file {} \;
```
Output:
```

./-file03: DOS executable (COM), start instruction 0x8c887e10 c3ee96c9
./-file02: data
./-file07: ASCII text
./-file00: data
./-file04: data
./-file09: data
./-file05: data
./-file08: data
./-file06: data
./-file01: data
```
Notice that -file07 is identified as ASCII text — that's the only human-readable file!
### Step 6: Read the human-readable file
```bash

bandit4@bandit:~/inhere$ cat ./-file07
```
Output:
```

4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

### Step 7: Log into Level 5
```bash

ssh bandit5@bandit.labs.overthewire.org -p 2220
```
Password: 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
