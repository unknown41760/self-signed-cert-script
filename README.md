# Script for installing the 3x‑UI panel for VLESS and 10‑year certificates

## Based on 
Antenka's code from [repo].(https://github.com/anten-ka/self-signed-cert-script-by-antenka)

## 📚 Description
This script automatically installs:

The 3X‑UI panel for managing VPN protocols.
A self‑signed SSL certificate valid for 10 years.

## 🛠️ What will be installed?

OpenSSL
qrencode
3X‑UI

## 🚀 How to use?

### 1. Clone the repository

```bash
sudo apt update && sudo apt install -y git curl openssl qrencode systemd && rm -rf ~/self-signed-cert-script && git clone https://github.com/unknown41760/self-signed-cert-script.git && cd self-signed-cert-script && chmod +x self_signed_cert.sh && sudo ./self_signed_cert.sh