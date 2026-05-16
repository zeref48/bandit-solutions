# 🔓 Level 8 → Level 9 — Finding Unique Lines with sort and uniq

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit8` |
| **Password** | `dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc` (from Level 7) |

---

## 🎯 Challenge

> The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only once

**Commands you may need:** `grep`, `sort`, `uniq`, `strings`, `base64`, `tr`, `tar`, `gzip`, `bzip2`, `xxd`

**Helpful Reading Material:**
- [Piping and Redirection](https://www.gnu.org/software/bash/manual/html_node/Redirections.html)

---

## 🧠 Understanding the Challenge

This level introduces the `sort` and `uniq` commands, which are essential for finding unique or duplicate lines in files.

### The `sort` Command

`sort` arranges lines in alphabetical or numerical order:

```bash
sort [options] [file]
```
## 💡 Solution
### Step 1: Connect to Level 8
```bash

ssh bandit8@bandit.labs.overthewire.org -p 2220
```
Password: dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
### Step 2: Check what files are in the home directory
```bash

bandit8@bandit:~$ ls -al
```
Output:
```

total 56
drwxr-xr-x   2 root    root     4096 Apr  3 15:18 .
drwxr-xr-x 150 root    root     4096 Apr  3 15:20 ..
-rw-r--r--   1 root    root      220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root    root     3851 Apr  3 15:10 .bashrc
-rw-r-----   1 bandit9 bandit8 33033 Apr  3 15:18 data.txt
-rw-r--r--   1 root    root      807 Mar 31  2024 .profile
```
There's a file named data.txt (about 33KB in size).
### Step 3: Find the unique line

The complete pipeline:
```bash

bandit8@bandit:~$ cat data.txt | sort | uniq -u
```
Breakdown of the pipeline:
```bash

cat data.txt | sort | uniq -u
│             │      │
│             │      └── show only unique lines
│             └── sort all lines alphabetically (brings duplicates together)
└── output the file contents to the pipe
```
Or more efficiently (avoiding unnecessary cat):
```bash

bandit8@bandit:~$ sort data.txt | uniq -u
```
### Step 4: Get the password

Output:
```

4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
```


### Step 6: Log into Level 9
```bash

ssh bandit9@bandit.labs.overthewire.org -p 2220
```
Password: 4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
