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


