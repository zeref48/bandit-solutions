# 🔓 Level 15 → Level 16 — SSL/TLS Encrypted Connections

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit15` |
| **Password** | `8xCjnmgoKbGLhHFAZlGE5Tmu4M2tKJQo` (from Level 14) |

---

## 🎯 Challenge

> The password for the next level can be retrieved by submitting the password of the current level to port **30001** on **localhost** using **SSL/TLS encryption**.
>
> **Helpful note:** Getting "DONE", "RENEGOTIATING" or "KEYUPDATE"? Read the "CONNECTED COMMANDS" section in the manpage.

**Commands you may need:** `ssh`, `telnet`, `nc`, `ncat`, `socat`, `openssl`, `s_client`, `nmap`, `netstat`, `ss`

**Helpful Reading Material:**
- [Secure Socket Layer/Transport Layer Security on Wikipedia](https://en.wikipedia.org/wiki/Transport_Layer_Security)
- [OpenSSL Cookbook - Testing with OpenSSL](https://www.feistyduck.com/library/openssl-cookbook/online/ch-testing-with-openssl.html)

---

## 🧠 Understanding the Challenge

This level is similar to the previous one, but the connection must be **encrypted** using SSL/TLS.

### What is SSL/TLS?

SSL (Secure Sockets Layer) and TLS (Transport Layer Security) are protocols that encrypt network communication:

| Without SSL/TLS | With SSL/TLS |
|----------------|--------------|
| Data sent in plain text | Data is encrypted |
| Anyone can read it | Only the intended recipient can read it |
| `nc` or `telnet` can connect | Needs special client like `openssl s_client` |

### The `openssl s_client` Command

`openssl s_client` is a generic SSL/TLS client for testing encrypted connections:

```bash
openssl s_client -connect host:port
```
