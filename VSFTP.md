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
### List Available Zones
```bash
firewall-cmd --get-zones
```
### View Current Rules (Default Zone)
```bash
firewall-cmd --list-all
```

### List Available Services
```bash
firewall-cmd --get-services
```

### Allow FTP Service (Recommended)
```bash
firewall-cmd --add-service=ftp --permanent
firewall-cmd --reload
```
### ❌ Disable Firewall (LAB ONLY – NOT RECOMMENDED)
```bash
systemctl stop firewalld
```

# VSFTPD Server Configuration
### Install VSFTPD
```bash
dnf install vsftpd -y
```
### Start and Enable VSFTPD
```bash
systemctl restart vsftpd
systemctl enable vsftpd
systemctl is-active vsftpd

```

### Verify FTP Ports Are Listening
```bash
lsof -i:21
```

### Create Files for FTP Sharing (Anonymous)
```bash
cd /var/ftp
touch file{1..10}.txt
```

### Anonymous FTP Configuration
#### Edit the VSFTPD configuration file:
```bash
vim /etc/vsftpd/vsftpd.conf
```

#### Ensure the following settings:
```bash
anonymous_enable=YES
local_enable=YES
write_enable=NO
anon_upload_enable=NO
anon_mkdir_write_enable=NO
```

### Restart Service
```bash
systemctl restart vsftpd
```

### Authenticated User FTP Configuration

#### Create a user (if not existing):
```bash
useradd kiosk
passwd kiosk
```

#### Ensure home directory permissions:
```bash
chmod 755 /home/kiosk
```
#### Login directory for user:
```bash
/home/kiosk
```

### FTP Client Configuration
#### Install FTP Client
dnf install ftp -y

#### Connect as Authenticated User
ftp <SERVER_IP>


#### Example session:

Connected to 192.168.206.100
Name: kiosk
Password:
230 Login successful


#### Check directory:

pwd


#### Output:

"/home/kiosk"

#### Connect as Anonymous User
ftp <SERVER_IP>


#### Login:

Name: ftp
Password: (press Enter)


#### Expected directory:

"/"

