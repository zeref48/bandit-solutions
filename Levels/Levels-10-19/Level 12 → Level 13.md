# 🔓 Level 12 → Level 13 — Hex Dumps and Repeated Compression

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit12` |
| **Password** | `7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4` (from Level 11) |

---

## 🎯 Challenge

> The password for the next level is stored in the file **data.txt**, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work. Use mkdir with a hard to guess directory name. Or better, use the command "mktemp -d". Then copy the datafile using cp, and rename it using mv (read the manpages!)

**Commands you may need:** `grep`, `sort`, `uniq`, `strings`, `base64`, `tr`, `tar`, `gzip`, `bzip2`, `xxd`, `mkdir`, `cp`, `mv`, `file`

**Helpful Reading Material:**
- [Hex dump on Wikipedia](https://en.wikipedia.org/wiki/Hex_dump)

---

## 🧠 Understanding the Challenge

This level involves multiple steps of decompression and introduces several important commands.

### Key Concepts

| Concept | Explanation |
|---------|-------------|
| **Hex dump** | A representation of binary data in hexadecimal format |
| **`xxd` command** | Creates hex dumps and reverses them (convert hex back to binary) |
| **`file` command** | Identifies file types (compressed, tar, etc.) |
| **`mv` command** | Renames or moves files |
| **`cp` command** | Copies files |
| **Working in /tmp** | Avoid cluttering your home directory |

### Common Compression Formats

| Extension | Format | Decompression Command |
|-----------|--------|----------------------|
| `.gz` | gzip | `gunzip file.gz` or `gzip -d file.gz` |
| `.bz2` | bzip2 | `bunzip2 file.bz2` or `bzip2 -d file.bz2` |
| `.tar` | Tape archive | `tar xf file.tar` |
| `.zip` | Zip | `unzip file.zip` |

### The Process

1. Create a working directory in `/tmp`
2. Copy `data.txt` to the working directory
3. Reverse the hex dump to get the original binary file
4. Identify the compression type using `file`
5. Decompress repeatedly until you get a text file
6. The password will be in the final decompressed file

---

## 💡 Solution

### Step 1: Connect to Level 12

```bash
ssh bandit12@bandit.labs.overthewire.org -p 2220
```
Password: 7x16WNeHIi5YkIhWsfFIqoognUTyj9Q4
### Step 2: Create a working directory in /tmp
```bash

bandit12@bandit:~$ mktemp -d
```
Output:
```

/tmp/tmp.XvN1qYz3ZP
```
Save this path or change into it:
```

bandit12@bandit:~$ cd $(mktemp -d)
```
Or:
```bash

bandit12@bandit:~$ mkdir /tmp/bandit12_work
bandit12@bandit:~$ cd /tmp/bandit12_work
```
### Step 3: Copy the data.txt file to your working directory
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ cp ~/data.txt .
```
### Step 4: Examine the file
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ ls -la
-rw-r----- 1 bandit12 bandit12 2714 Apr  3 15:18 data.txt

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ file data.txt
data.txt: ASCII text
```
### Step 5: Reverse the hex dump to get binary file

The xxd command can reverse a hex dump with the -r option:
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ xxd -r data.txt > data.bin
```
Now check the file type:
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ file data.bin
data.bin: gzip compressed data, was "data2.bin", last modified: ...
```
It's a gzip file!
### Step 6: Decompress repeatedly
#### Round 1: gzip

Rename to have the correct extension:
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ mv data.bin data.gz
bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ gunzip data.gz
```
Check the new file:
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ ls
data

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ file data
data: bzip2 compressed data, block size = 900k
```
#### Round 2: bzip2
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ mv data data.bz2
bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ bunzip2 data.bz2
```
Check:
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ file data
data: gzip compressed data, was "data4.bin", last modified: ...
```
#### Round 3: gzip again
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ mv data data.gz
bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ gunzip data.gz
```
Check:
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ file data
data: POSIX tar archive (GNU)
```
#### Round 4: tar
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ tar xf data
```
This extracts the contents. Check what was extracted:
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ ls
data  data5.bin
```
Check the new file:
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ file data5.bin
data5.bin: POSIX tar archive (GNU)
```
#### Round 5: tar again
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ tar xf data5.bin
```
Check what was extracted:
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ ls
data  data5.bin  data6.bin
```
Check the new file:
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ file data6.bin
data6.bin: bzip2 compressed data, block size = 900k
```
#### Round 6: bzip2 again
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ mv data6.bin data6.bz2
bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ bunzip2 data6.bz2
```
Check:
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ file data6
data6: POSIX tar archive (GNU)
```
#### Round 7: tar again
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ tar xf data6
```
Check what was extracted:
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ ls
data  data5.bin  data6  data8.bin
```
Check the new file:
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ file data8.bin
data8.bin: gzip compressed data, was "data9.bin", last modified: ...
```
#### Round 8: gzip again
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ mv data8.bin data8.gz
bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ gunzip data8.gz
```
Check:
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ file data8
data8: ASCII text
```
### Step 7: Read the final file
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ cat data8
```
Output:
```

The password is FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
```


### Step 8: Log into Level 13
```bash

ssh bandit13@bandit.labs.overthewire.org -p 2220
```
Password: FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn
### Step 9: Clean up (optional)
```bash

bandit12@bandit:/tmp/tmp.XvN1qYz3ZP$ cd ~
bandit12@bandit:~$ rm -rf /tmp/tmp.XvN1qYz3ZP
```
