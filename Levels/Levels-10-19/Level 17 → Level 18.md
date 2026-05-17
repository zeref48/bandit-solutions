# 🔓 Level 17 → Level 18 — Comparing Files with diff

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit17` |
| **Password** | Use the SSH private key from Level 16 |

**Credentials:** `ssh -i bandit17_key bandit17@bandit.labs.overthewire.org -p 2220`

---

## 🎯 Challenge

> There are 2 files in the homedirectory: **passwords.old** and **passwords.new**. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new
>
> **NOTE:** if you have solved this level and see 'Byebye!' when trying to log into bandit18, this is related to the next level, bandit19

**Commands you may need:** `cat`, `grep`, `ls`, `diff`

---

## 🧠 Understanding the Challenge

This level introduces the `diff` command, which compares files line by line and shows the differences.

### The `diff` Command

`diff` compares files and displays the lines that differ:

```bash
diff file1 file2
