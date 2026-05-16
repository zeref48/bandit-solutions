# 🔓 Level 13 → Level 14 — Using SSH Private Keys

## 📊 Level Info

| Property | Value |
|----------|-------|
| **Host** | `bandit.labs.overthewire.org` |
| **Port** | `2220` |
| **Username** | `bandit13` |
| **Password** | `FO5dwFsc0cbaIiH0h8J2eUks2vdTDwAn` (from Level 12) |

---

## 🎯 Challenge

> The password for the next level is stored in **/etc/bandit_pass/bandit14** and can only be read by user bandit14. For this level, you don't get the next password, but you get a private SSH key that can be used to log into the next level. Look at the commands that logged you into previous bandit levels, and find out how to use the key for this level.
> 
> If you need help with this level: a hint file can be found in the home directory.
> Make sure to read the error messages as they are informative.

**Commands you may need:** `ssh`, `scp`, `umask`, `chmod`, `cat`, `nc`, `install`

**Helpful Reading Material:**
- [SSH/OpenSSH/Keys](https://en.wikipedia.org/wiki/SSH_(Secure_Shell))
- [Transferring Files via SCP](https://www.geeksforgeeks.org/scp-command-in-linux-with-examples/)

---

## 🧠 Understanding the Challenge

This level introduces **SSH key authentication** as an alternative to password authentication.

### SSH Key Authentication

Instead of using a password, you can use a **key pair**:
- **Private key** (keep secret, like a password)
- **Public key** (placed on the server)

If your private key matches the public key on the server, you can log in without a password.

### Key Files

| File | Purpose |
|------|---------|
| `id_rsa` | Private key (keep secret, permissions 600) |
| `id_rsa.pub` | Public key (can be shared) |
| `authorized_keys` | List of public keys allowed to log in |

### Using an SSH Key

```bash
ssh -i private_key_file username@host -p port
