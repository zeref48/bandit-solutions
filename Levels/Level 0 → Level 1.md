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
