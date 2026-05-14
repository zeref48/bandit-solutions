
# 🔓 Level 0 — First Connection

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit0` |
| **Password** | `bandit0` |

---

## 🎯 Challenge

> The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

**Commands you may need:** `ssh`

---

## 🧠 What is SSH?

**SSH** (Secure Shell) is a network protocol that lets you securely connect to and control a remote computer over an unsecured network.

Think of it like a **secure tunnel** between your computer and the Bandit server. Everything you type and see is encrypted, so no one can spy on your connection.

### SSH Syntax Breakdown

```bash
ssh [username]@[hostname] -p [port] bash
```

## 💡 Solution

<u>Step 1: Connect via SSH</u>

Open your terminal (Linux/Mac) or Command Prompt/PowerShell with SSH enabled (Windows 10+), then type:
```bash

ssh bandit0@bandit.labs.overthewire.org -p 2220
```
Step 2: Accept the host key

When prompted about host authenticity, type yes and press Enter:
text
```
The authenticity of host '[bandit.labs.overthewire.org]:2220 ([13.63.65.121]:2220)' can't be established.
ED25519 key fingerprint is: SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[bandit.labs.overthewire.org]:2220' (ED25519) to the list of known hosts.
```
Step 3: Enter the password
text
```
bandit0@bandit.labs.overthewire.org's password: bandit0
```
    ⚠️ Note: Nothing will show on screen as you type the password. No asterisks, no dots. This is normal for security.

Step 4: Welcome message

After successful login, you'll see the OverTheWire welcome banner:
text
```
                         _                     _ _ _   
                        | |__   __ _ _ __   __| (_) |_ 
                        | '_ \ / _` | '_ \ / _` | | __|
                        | |_) | (_| | | | | (_| | | |_ 
                        |_.__/ \__,_|_| |_|\__,_|_|\__|
                                                       

                      This is an OverTheWire game server. 
            More information on http://www.overthewire.org/wargames

backend: gibson-0

      ,----..            ,----,          .---.
     /   /   \         ,/   .`|         /. ./|
    /   .     :      ,`   .'  :     .--'.  ' ;
   .   /   ;.  \   ;    ;     /    /__./ \ : |
  .   ;   /  ` ; .'___,/    ,' .--'.  '   \' .
  ;   |  ; \ ; | |    :     | /___/ \ |    ' '
  |   :  | ; | ' ;    |.';  ; ;   \  \;      :
  .   |  ' ' ' : `----'  |  |  \   ;  `      |
  '   ;  \; /  |     '   :  ;   .   \    .\  ;
   \   \  ',  /      |   |  '    \   \   ' \ |
    ;   :    /       '   :  |     :   '  |--"
     \   \ .'        ;   |.'       \   \ ;
  www. `---` ver     '---' he       '---" ire.org

Welcome to OverTheWire!
```
If you find any problems, please report them to the #wargames channel on
discord or IRC.

Step 5: Find the password for Level 1

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
text
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
text

```Congratulations on your first steps into the bandit game!!
Please make sure you have read the rules at https://overthewire.org/rules/
If you are following a course, workshop, walkthrough or other educational activity,
please inform the instructor about the rules as well and encourage them to
contribute to the OverTheWire community so we can keep these games free!

The password you are looking for is: ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```
Step 6: Log out

When you're done, exit the SSH session:
```bash

bandit0@bandit:~$ exit
```

