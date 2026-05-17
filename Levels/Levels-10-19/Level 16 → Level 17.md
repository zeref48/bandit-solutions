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
