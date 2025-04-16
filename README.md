# 🌐 Cloud-Based OS Access via Web Browser

**Access a fully functional Kali Linux OS through your browser — powered by Ubuntu Desktop, noVNC, and pure network engineering.**

This project is a practical implementation of Desktop Virtualization in a Cloud Computing context. The idea is simple: run an operating system inside a host machine (Ubuntu Desktop) as a headless virtual machine (Kali Linux) and make it remotely accessible over a browser using VNC + noVNC + Websockify. This allows users to experience an OS without the need to install it natively.



## 🚀 Project Objective

Enable access to a Kali Linux VM from a **web browser**, running on an Ubuntu Desktop host. The system supports lightweight, GUI-based interactions without dual-booting or full hardware virtualization.

This system can help:
- Students learn Linux-based tools and commands.
- Developers test tools across OSes.
- Teams collaborate on a centralized system.
- Organizations implement lightweight VDI (Virtual Desktop Infrastructure) over LAN/Wi-Fi.


## 🛠️ Technologies & Tools Used

| Category          | Tools / Technologies                           |
|-------------------|-------------------------------------------------|
| Virtualization    | QEMU/KVM, Oracle Virtual Box, Headless Mode     |
| Remote Access     | VNCServer, noVNC, Websockify                    |
| Networking        | Netplan, IP Configuration, Firewalls            |
| Web Server        | Nginx                                           |
| Tunneling (Tried) | Ngrok, Reverse SSH (Explored but not included)  |
| Scripting         | Shell (manual commands)                         |

---

## 🧠 What I Learned

- 📡 Networking with `netplan`, firewall configuration, port management.
- 🔐 Handling authentication with VNC and OS-level logins.
- ⚙️ Installing and managing headless VMs.
- 🌍 Running Nginx web servers and exposing them via Ngrok.
- 🤯 Troubleshooting nested virtualization, promiscuous mode issues, and display servers.

---

## 🧭 Project Journey (The Backstory)

1. **Early Experiments:**
   - Started with Ubuntu Server (CLI-only) on VirtualBox.
   - Learned **SSH**, **Nginx**, **Ngrok**, and hosted static webpages.
   - Tried enabling virtualization with `gdm3`, but **hardware didn’t support nested virtualization**.

2. **VMWare Phase:**
   - Rebuilt entire system on VMWare.
   - Installed Kali Linux VM and tried **VNCServer**, **Apache Guacamole**, **X11VNC**, and even **Shellinabox**, **ttyd**, and **Wetty**.
   - Faced consistent failure due to **promiscuous mode restrictions**, which broke bridged network between host and VMs.

3. **Breakthrough:**
   - Switched to **Ubuntu Desktop** as base OS.
   - Successfully ran Kali Linux using **Virtual Box** in **headless mode**.
   - Setup **VNCServer**, **noVNC**, and **Websockify** to expose the GUI in the browser.

---

## ⚙️ Implementation Steps

### 🔧 1. VM Configuration
- Run the Kali Linux VM in headless mode to prevent display conflict:
  ```bash
  vncserver :1 -localhost no
  

### 🧵 2. Websockify + noVNC
- After installing `pip3`, install websockify:
  ```bash
  pip3 install websockify
  
- Start Websockify bridge to convert VNC stream for browser access:
  ```bash
  websockify --web ~/noVNC 6080 localhost:5901
  

### 🔥 3. Network Configuration
- Assign static IPs to host and guest using `netplan`.
- Disable the firewall on Kali (during testing).
- Set up bridged networking for VMs.

### 🧱 4. (Attempted) Nginx Proxy to VNC
- Tried forwarding VNC stream using Nginx's `proxy_pass`. This failed due to websocket incompatibilities.

---

## 🔐 Security Notes

- Authentication is **two-layered**:
  - Linux login credentials (username/password).
  - VNC server password.
- Access limited to same network (for now).
- Can be extended using **Tailscale**, **WireGuard**, or VPNs for secure remote access.

---

## 📸 Screenshots

*Refer to the “screenshots” folder in the repo for detailed visuals of each stage:*
- Ubuntu Desktop with running VNC session.
- Browser-based noVNC session showing Kali Linux.
- Terminal setup and IP configs.

---

## 🔮 Future Work

- Full **VDI System** across LAN for multiple users.
- VPN or ZeroTier/Tailscale support for access from anywhere.
- Nginx-authenticated dashboard for multi-VM access.
- Multi-user authentication and permission control.

---

## 📂 Repository Contents

| File / Folder              | Description                             |
|---------------------------|-----------------------------------------|
| `nginx-configurations/`   | Server block configs and proxy setups   |
| `network-configurations/` | Netplan `.yaml` files for IP setup      |
| `Server-WebPages/`        | Simple webpages served via Nginx        |
| `screenshots/`            | Screenshots of VNC and browser setup    |
| `README.md`               | This documentation 😄                   |

---


## 🙌 Acknowledgement

Huge learning curve. Countless weekends.  
Multiple resets.  
And finally, a working cloud-ready OS on browser.  
If this repo helps even one person — mission accomplished. ❤️

---
```
> Built with ☕, 🧠, and a whole lot of 🔄 trial & error.
