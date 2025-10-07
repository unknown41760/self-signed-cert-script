# Script for installing the 3x‑UI panel for VLESS and 10‑year certificates

## Based on 
Antenka's code from repo https://github.com/anten-ka/self-signed-cert-script-by-antenka

## 📚 Description
This script automatically installs:

The 3X‑UI panel for managing VPN protocols.
A self‑signed SSL certificate valid for 10 years.

## 🛠️ What will be installed?

OpenSSL
qrencode
3X‑UI

## Secure server beforehand

### 🔑 1. Secure SSH Access

```bash
# Edit the SSH daemon configuration
sudo nano /etc/ssh/sshd_config
```

#### Change the default SSH port

(Replace `2222` with whatever port you wish to use.)

```yaml
# Inside /etc/ssh/sshd_config
Port 2222
```

```bash
# Restart SSH to apply changes
sudo systemctl restart ssh
```

#### Disable root login

```bash
# Inside /etc/ssh/sshd_config
PermitRootLogin no
```

#### Use SSH keys instead of passwords

```bash
# On your local machine
ssh-keygen -t ed25519
```

```bash
# Copy the public key to the VPS (adjust port if you changed it)
ssh-copy-id -p 2222 user@your-vps-ip
```

#### Disable password authentication

```bash
# Inside /etc/ssh/sshd_config
PasswordAuthentication no
```

### 🛡️ 2. Firewall Setup

#### Ubuntu / Debian (UFW)

```bash
# Allow the new SSH port
sudo ufw allow 2222/tcp
sudo ufw enable
sudo ufw status
```

#### CentOS / RedHat (firewalld)

```bash
# Add the new SSH port permanently
sudo firewall-cmd --permanent --add-port=2222/tcp
sudo firewall-cmd --reload
```

### 🔐 3. Keep System Updated

#### Debian / Ubuntu

```bash
sudo apt update && sudo apt upgrade -y
```

#### CentOS / RHEL

```bash
sudo yum update -y
```

### 🚨 4. Install Fail2Ban

```bash
# Install
sudo apt install fail2ban -y   # Debian/Ubuntu
sudo yum install fail2ban -y   # CentOS/RHEL
```

```bash
# Enable and start the service
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

### 🔍 5. Monitor Users & Processes

```bash
# Create a non‑root user
adduser myuser
usermod -aG sudo myuser   # Ubuntu – add to sudo group
```

```bash
# Check logs
sudo journalctl -xe
sudo tail -f /var/log/auth.log
```

### 🧰 6. Optional but Recommended

```bash
# Install intrusion detection tools
sudo apt install rkhunter chkrootkit   # Debian/Ubuntu
sudo yum install rkhunter chkrootkit   # CentOS/RHEL
```

```bash
# Enable automatic security updates (Ubuntu/Debian)
sudo apt install unattended-upgrades
```

```bash
# Enable two‑factor authentication for SSH
sudo apt install libpam-google-authenticator
# Then configure /etc/pam.d/sshd and /etc/ssh/sshd_config accordingly
```

**Tip:** After any change to `sshd_config`, always verify the syntax before restarting:

```bash
sudo sshd -t
```

If it reports `syntax OK`, you can safely restart.


## 🚀 How to use?

### 1. Clone the repository

```bash
sudo apt update && sudo apt install -y git curl openssl qrencode systemd && rm -rf ~/self-signed-cert-script && git clone https://github.com/unknown41760/self-signed-cert-script.git && cd self-signed-cert-script && chmod +x self_signed_cert.sh && sudo ./self_signed_cert.sh
```
