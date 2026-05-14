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
