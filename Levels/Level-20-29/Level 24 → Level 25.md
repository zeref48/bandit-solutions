# 🔓 Level 24 → Level 25 — Brute-Forcing a PIN Code

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit24` |
| **Password** | `gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8` (from Level 23) |

---

## 🎯 Challenge

> A daemon is listening on port **30002** and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.
>
> You do not need to create new connections each time.

**Commands you may need:** `ssh`, `nc`, `cat`, `bash`, `screen`, `tmux`, `for` loops, `while` loops

---

## 🧠 Understanding the Challenge

This level introduces **brute-forcing** - trying all possible combinations until one works.

### The Setup

There's a service running on port `30002` that:
- Expects input in the format: `[bandit24_password] [4-digit_pincode]`
- If the pincode is correct, it returns the password for bandit25
- If incorrect, it returns an error message

### The Numbers

- 4-digit pincode ranges from `0000` to `9999`
- That's **10,000 possible combinations**
- We need to try them all

### Optimization

The note says: *"You do not need to create new connections each time"*

This means we can:
1. Open ONE connection to the service
2. Send multiple attempts through the same connection
3. This is much faster than opening 10,000 separate connections

---

## 💡 Solution

### Step 1: Connect to Level 24

```bash
ssh bandit24@bandit.labs.overthewire.org -p 2220
