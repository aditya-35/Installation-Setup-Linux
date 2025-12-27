# VSFTPD Full Configuration Guide with Firewalld (RHEL / CentOS)

This repository documents the **complete configuration of VSFTPD (Very Secure FTP Daemon)** along with **Firewalld** on RHEL-based Linux systems.

> ⚠️ WARNING  
> FTP is **NOT secure** (credentials are sent in plain text).  
> This guide is intended for **learning, labs, and exams (RHCSA/RHCE)**.  
> For production, use **SFTP (SSH File Transfer Protocol)**.

---

## Table of Contents

- [System Information](#system-information)
- [Firewall Management](#firewall-management)
- [VSFTPD Server Configuration](#vsftpd-server-configuration)
- [Anonymous FTP Configuration](#anonymous-ftp-configuration)
- [FTP Client Configuration](#ftp-client-configuration)
- [Verification & Testing](#verification--testing)
- [Security Notes](#security-notes)
- [Best Practices](#best-practices)

---

## System Information

**Server OS:** RHEL / CentOS / Rocky / Alma  
**Packages Used:**  
- `vsftpd`
- `ftp`
- `firewalld`

**Important Paths:**

| Item | Path |
|---|---|
| VSFTPD Config | `/etc/vsftpd/vsftpd.conf` |
| Anonymous FTP Root | `/var/ftp` |
| User FTP Root | `/home/USER` |

**Ports:**
- FTP Control: `21`
- FTP Data: `20`

---

## Firewall Management

### Install Firewalld

```bash
dnf install firewalld -y
```

### Start and Enable Firewalld

```bash
systemctl start firewalld
systemctl enable firewalld
systemctl is-active firewalld
systemctl is-enabled firewalld
```
