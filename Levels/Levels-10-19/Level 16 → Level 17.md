
# 🔓 Level 16 → Level 17 — Port Scanning with nmap

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit16` |
| **Password** | `kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx` (from Level 15) |

---

## 🎯 Challenge

> The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range **31000 to 32000**. First find out which of these ports have a server listening on them. Then find out which of those speak SSL/TLS and which don't. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.
>
> **Helpful note:** Getting "DONE", "RENEGOTIATING" or "KEYUPDATE"? Read the "CONNECTED COMMANDS" section in the manpage.

**Commands you may need:** `ssh`, `telnet`, `nc`, `ncat`, `socat`, `openssl`, `s_client`, `nmap`, `netstat`, `ss`

**Helpful Reading Material:**
- [Port scanner on Wikipedia](https://en.wikipedia.org/wiki/Port_scanner)

---

## 🧠 Understanding the Challenge

This level introduces **port scanning** to find open ports, then testing each to see if it speaks SSL/TLS.

### Port Scanning with `nmap`

`nmap` (Network Mapper) is a powerful port scanning tool:

```bash
nmap [options] target -p port-range
```
## 💡 Solution
### Step 1: Connect to Level 16
```bash

ssh bandit16@bandit.labs.overthewire.org -p 2220
```
Password: kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx
### Step 2: Scan ports 31000-32000 using nmap
```bash

bandit16@bandit:~$ nmap -p 31000-32000 localhost
```
Output:
```

Starting Nmap 7.94SVN ( https://nmap.org ) at 2026-05-17 08:18 UTC
Nmap scan report for localhost (127.0.0.1)
Host is up (0.00014s latency).
Not shown: 996 closed tcp ports (conn-refused)
PORT      STATE SERVICE
31046/tcp open  unknown
31518/tcp open  unknown
31691/tcp open  unknown
31790/tcp open  unknown
31960/tcp open  unknown

Nmap done: 1 IP address (1 host up) scanned in 0.07 seconds
```
The open ports are: 31046, 31518, 31691, 31790, 31960
### Step 3: Test each port for SSL/TLS
Test port 31046 (NOT SSL):
```bash

bandit16@bandit:~$ echo "kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx" | openssl s_client -connect localhost:31046 -quiet
```
Output: SSL error - not an SSL/TLS port
Test port 31518 (SSL but just echoes back):
```bash

bandit16@bandit:~$ echo "kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx" | openssl s_client -connect localhost:31518 -quiet

