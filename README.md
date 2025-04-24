# 🛡️ OpenWRT/RaspAP Integrated Raspberry Pi VPN Router

A portable, secure, customizable VPN router built using **Raspberry Pi 4**, **OpenWRT**, and **RaspAP**. Designed for privacy-conscious users, digital nomads, and cybersecurity enthusiasts, this project offers encrypted internet access, ad blocking, and full control over network configuration — all in your pocket.

## 📌 Project Overview

This project transforms a Raspberry Pi into a powerful, open-source VPN router with built-in support for:
- Encrypted browsing via OpenVPN
- DNS-level ad-blocking via AdGuard Home
- Full network monitoring and control via OpenWRT
- Web-based and SSH configuration access
- Portable design, perfect for travel or remote work

Whether you're browsing in a coffee shop, working from a hotel, or building a secure IoT environment — this router keeps your data private and your experience clean.

## ⚙️ Features

- 🔒 VPN Tunneling using OpenVPN
- 🚫 Ad Blocking with AdGuard Home
- 🧠 Custom Firewall rules for secure routing
- 🌐 LAN + WAN Segregation with NAT
- 🧩 Web GUI and SSH access
- 🛠️ Easy configuration backups
- 🧳 Lightweight and travel-ready

## 🧰 Hardware Requirements

- Raspberry Pi 4 Model B
- Reliable 5V Power Supply or Power Bank
- MicroSD Card (32GB or more)
- USB WiFi Adapter (for secondary interface)
- Ethernet Cable (optional)
- Optional: 3D Printed Case

## 🧱 Software Stack

- OpenWRT – Open-source router OS
- RaspAP – Web UI for WiFi management
- AdGuard Home – Network-wide ad blocker
- OpenVPN – VPN tunneling
- dnsmasq & hostapd – DHCP and WiFi access point
- iptables – NAT and firewall control

## 🛠️ Step-by-Step Installation Guide

### 1️⃣ Flash OpenWRT

- Download OpenWRT for Raspberry Pi 4 from https://openwrt.org
- Flash using Raspberry Pi Imager or Balena Etcher
- Insert SD card and boot Raspberry Pi

### 2️⃣ Expand Partition (Linux GParted)

- Insert SD card into a Linux PC
- Open GParted
- Locate `/dev/mmcblk0p2` and resize to full card capacity
- Apply changes and safely eject

### 3️⃣ Connect and Access

- Connect Pi to PC via Ethernet or USB adapter
- Set PC IP manually (e.g., 192.168.1.10)
- SSH into Pi:ssh root@192.168.1.1 Password: OPENWRT/RASPAP

### 4️⃣ Backup Config Files

- cd /etc/config cat <<EOF > env.sh #!/bin/sh cp /etc/config/network /etc/config/network.bak cp /etc/config/firewall /etc/config/firewall.bak cp /etc/config/wireless /etc/config/wireless.bak EOF chmod +x env.sh ./env.sh

### 5️⃣ Replace Config Files

Edit or replace the following manually:
- `/etc/config/network`
- `/etc/config/firewall`
- `/etc/config/wireless`

Use `vi` or `nano` for editing directly.

### 6️⃣ Access Web Interface

- Go to http://192.168.1.1
- Login: Username `root`, Password `OPENWRT/RASPAP`
- Change default password via **System > Administration**

### 7️⃣ VPN Setup (OpenVPN)

- opkg update opkg install openvpn-openssl luci-app-openvpn
- Upload or configure `.ovpn` files in `/etc/openvpn/`
- Enable and start the VPN interface

### 8️⃣ Install AdGuard Home

- Download AdGuard Home ARM build from https://adguard.com
- Extract and install: tar -xvzf AdGuardHome_linux_arm.tar.gz cd AdGuardHome ./AdGuardHome -s install
- Access dashboard: http://10.71.71.1:3000

### 9️⃣ Final Network Setup

#### Sample Network Settings
- LAN IP: `10.71.71.1/24`
- WAN via `wlan1` (USB WiFi)
- VPN interface `tun0`

#### Firewall Zones
- `lan` → allow all
- `wan` → allow output only, NAT enabled
- `vpn` → route through `tun0`

#### Wireless Config
- SSID: `SecurePiRouter`
- WPA2 encryption, Channel 6
- Interface bridged with `br-lan`

### 🔁 Reboot and Test

reboot

After reboot:
- Web: http://10.71.71.1
- SSH: `ssh root@10.71.71.1`
- Run: `curl ifconfig.me` to check VPN
- Visit any ad-heavy site to test ad blocking

## 📦 Use Cases

- 🧳 Travel Router
- 🏠 Home Secure Network
- 📡 IoT Gateway
- 👨‍👩‍👧 Parental Controls
- 🔐 Cybersecurity Education

Contact Information :
1. Ben Tom Abey - 
2. Gouri Nandana A - nandanagouri47@gmail.com
3. Bennet Binu Varghese - 


