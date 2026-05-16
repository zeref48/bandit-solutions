# 🔓 Level 14 → Level 15 — Sending Data Over TCP with netcat

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit14` |
| **Password** | `MU4VWeTyJk8ROof1qqmcBPaLh7lDCPvS` (from Level 13) |

---

## 🎯 Challenge

> The password for the next level can be retrieved by submitting the password of the current level to port **30000** on **localhost**.

**Commands you may need:** `ssh`, `telnet`, `nc`, `openssl`, `s_client`, `nmap`

**Helpful Reading Material:**
- [How the Internet works in 5 minutes (YouTube)]()
- [IP Addresses](https://en.wikipedia.org/wiki/IP_address)
- [Localhost on Wikipedia](https://en.wikipedia.org/wiki/Localhost)
- [Ports on Wikipedia](https://en.wikipedia.org/wiki/Port_(computer_networking))

---

## 🧠 Understanding the Challenge

This level introduces **network ports** and the `nc` (netcat) command to send data over TCP connections.

### What is a Port?

A port is a virtual endpoint for network communication. Think of an IP address as a street address, and ports as apartment numbers:

| Concept | Analogy |
|---------|---------|
| IP Address | Street address of a building |
| Port | Specific apartment number |
| Connection | Delivering a letter to that apartment |

### Common Port Ranges

| Range | Purpose |
|-------|---------|
| 0-1023 | Well-known ports (HTTP=80, SSH=22, HTTPS=443) |
| 1024-49151 | Registered ports |
| 49152-65535 | Dynamic/private ports |

### The `nc` (netcat) Command

`nc` (netcat) is a networking utility for reading/writing data across network connections:

```bash
nc [options] host port
