# 🔓 Level 0 → Level 1 — The readme File

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit0` |
| **Password** | `bandit0` |

---

## 🎯 Challenge

> The password for the next level is stored in a file called **readme** located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

**Commands you may need:** `ls`, `cd`, `cat`, `file`, `du`, `find`

> 💡 **TIP:** Create a file for notes and passwords on your local machine!
> 
> Passwords for levels are not saved automatically. If you do not save them yourself, you will need to start over from bandit0.
> 
> Passwords also occasionally change. It is recommended to take notes on how to solve each challenge. As levels get more challenging, detailed notes are useful to return to where you left off, reference for later problems, or help others after you've completed the challenge.

---

## 🧠 Understanding the Challenge

This level is straightforward — it introduces the basic commands you'll use throughout the Bandit wargame:

| Command | Purpose |
|---------|---------|
| `ls` | List files and directories |
| `cd` | Change directory |
| `cat` | Concatenate and display file contents |
| `file` | Determine file type |
| `du` | Estimate file space usage |
| `find` | Search for files in a directory hierarchy |

The password for Level 1 is simply waiting in a file named `readme` in the home directory. All we need to do is:

1. Connect as `bandit0`
2. Find the `readme` file
3. Read its contents
4. Use that password to connect as `bandit1`

---

## 💡 Solution

### Step 1: Connect to Level 0

Open your terminal and SSH into the game:

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

### Step 5: Find the password for Level 1

Once logged in, you'll see the prompt:
bash
```
bandit0@bandit:~$
```
List all files in your home directory:
bash
```
bandit0@bandit:~$ ls -la
```
Output:

```
total 24
drwxr-xr-x   2 root    root    4096 Apr  3 15:17 ./
drwxr-xr-x 150 root    root    4096 Apr  3 15:20 ../
-rw-r--r--   1 root    root     220 Mar 31  2024 .bash_logout
-rw-r--r--   1 root    root    3851 Apr  3 15:10 .bashrc
-rw-r--r--   1 root    root     807 Mar 31  2024 .profile
-rw-r-----   1 bandit1 bandit0  438 Apr  3 15:17 readme
```
Notice the file named readme — this contains the password for Level 1.

Read the file:
```bash

bandit0@bandit:~$ cat readme
```
Output:


```Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walkthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```
### Step 6: Log out

When you're done, exit the SSH session:
```bash

bandit0@bandit:~$ exit
```

