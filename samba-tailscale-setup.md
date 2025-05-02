# Raspberry Pi Homelab: Secure File Share Over VPN 🚀

This homelab project turned a basic Raspberry Pi into a secure, VPN-only, remote-access file sharing server—with lessons in Linux security, networking, and kernel debugging.

---

## 🏁 Getting Started

The project began by:
- Rebuilding the SD card with Raspberry Pi OS Lite
- Enabling wireless connectivity
- Connecting the Pi to a Tailscale VPN mesh

---

## Security Hardening

Once network access was stable, I focused on securing the system:

- 🔥 Configured `firewalld` to:
  - Block **all** incoming traffic except `SSH` and `SMB`
  - Allow **all** necessary outgoing traffic
- 🛡️ Set up `fail2ban` using `iptables`:
  - Only allow SSH access through the Tailscale network
  - Protect against brute force attempts
- 📵 Disabled Bluetooth and root SSH login
- 👤 Created a restricted SMB user (no `sudo`, no root access)

🔗 **See detailed Security documentation:**  
[Security Branch: fail2ban-firewall.md](https://github.com/AJprogramming123/Raspberry_Pi/tree/Security)

---

## 🛠️ VPN-Based File Sharing (Samba + Tailscale)

The centerpiece of the setup was building a **self-hosted file share** over a private VPN:

- Installed and configured `samba`
- Shared a specific folder with controlled access
- Enabled devices (phones, laptops, etc.) on the **Tailscale network** to access the share securely—anywhere with internet

It works like a personal Google Drive without cloud dependency.

🔗 **See full Samba + Tailscale configuration:**  
[Network Branch: samba-setup.md](https://github.com/AJprogramming123/Raspberry_Pi/tree/Network)

---

## Troubleshooting & Kernel Hurdles

Tried adding a new WiFi adapter—but hit a wall:

- Adapter not recognized (`uname -r` mismatch)
- Installed `raspberrypi-kernel-headers` manually
- Built and tested the driver...but:
  > 🧱 **Kernel not compatible. No stable workaround.**

Sometimes the right move is just to wait for the upstream fix.

🔗 **Troubleshooting log and commands:**  
[Troubleshoot Branch: wifi-driver.md](https://github.com/AJprogramming123/Raspberry-Pi/tree/Troubleshoot)

---

## 🧠 Key Takeaways

- 🔐 Layered security: firewall + VPN + fail2ban + user controls
- 🌐 Tailscale simplifies remote access with zero hassle NAT
- 🐧 Linux debugging teaches patience, precision, and persistence

---

## 📂 Related Work

| Branch | Description |
|--------|-------------|
| [`Security`](https://github.com/AJprogramming123/Raspberry_Pi/tree/Security) | Hardening SSH, firewall, and VPN access |
| [`Network`](https://github.com/AJprogramming123/Raspberry_Pi/tree/Network) | Samba setup and Tailscale integration |
| [`Troubleshoot`](https://github.com/AJprogramming123/Raspberry_Pi/tree/Troubleshoot) | Kernel header mismatch and driver install attempts |
