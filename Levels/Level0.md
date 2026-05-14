
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
ssh [username]@[hostname] -p [port]


💡 Solution
Step 1: Connect via SSH

Open your terminal (Linux/Mac) or Command Prompt/PowerShell with SSH enabled (Windows 10+), then type:
bash

ssh bandit0@bandit.labs.overthewire.org -p 2220

Step 2: Accept the host key

When prompted about host authenticity, type yes and press Enter:
text

The authenticity of host '[bandit.labs.overthewire.org]:2220 ([13.63.65.121]:2220)' can't be established.
ED25519 key fingerprint is: SHA256:C2ihUBV7ihnV1wUXRb4RrEcLfXC5CXlhmAAM/urerLY
This key is not known by any other names.
Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
Warning: Permanently added '[bandit.labs.overthewire.org]:2220' (ED25519) to the list of known hosts.

Step 3: Enter the password
text

bandit0@bandit.labs.overthewire.org's password: bandit0

    ⚠️ Note: Nothing will show on screen as you type the password. No asterisks, no dots. This is normal for security.

Step 4: Welcome message

After successful login, you'll see the OverTheWire welcome banner:
text

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

If you find any problems, please report them to the #wargames channel on
discord or IRC.
