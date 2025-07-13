# 🖥️ XRDP Setup + User Access + ICMP Configuration

## 🎯 Objective

This project focused on preparing a Linux system (Ubuntu/Kali) for remote desktop access via **XRDP**, creating a new sudo-enabled user, and configuring the system to allow **ICMP (ping)** traffic for connectivity diagnostics. The goal was to simulate a realistic admin or SOC setup scenario with secure remote access and proper firewall rules.

---

## 🧠 Skills Learned

- Installation and configuration of XRDP for GUI-based remote desktop
- Linux user and permission management (sudoers)
- Use of `iptables` for configuring inbound and outbound ICMP traffic
- Persistence of firewall rules across system reboots
- Practical system hardening and remote troubleshooting skills

---

## 🧰 Tools Used

- **XRDP** – Remote Desktop Protocol for Linux
- **iptables** – Linux firewall configuration
- **iptables-persistent** – Make rules survive reboot
- **Linux CLI** – Bash terminal for all operations
- **Ubuntu 22.04** – Base OS (also tested on Kali)

---

## 🪜 Steps

### ✅ System Update and XRDP Installation

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install xrdp -y

✅ Add XRDP to ssl-cert Group & Enable on Boot
bash
Copy
Edit
sudo adduser xrdp ssl-cert
sudo systemctl enable xrdp
sudo reboot
✅ Add New User and Grant Sudo Access
bash
Copy
Edit
sudo adduser Dipak
sudo usermod -aG sudo Dipak
su - Dipak
✅ Enable ICMP (Ping) Inbound and Outbound
bash
Copy
Edit
# Allow ping request (inbound)
sudo iptables -A INPUT -p icmp --icmp-type echo-request -j ACCEPT

# Allow ping response (outbound)
sudo iptables -A OUTPUT -p icmp --icmp-type echo-reply -j ACCEPT

# Allow outbound ping
sudo iptables -A OUTPUT -p icmp --icmp-type echo-request -j ACCEPT

# Allow ping reply back (inbound)
sudo iptables -A INPUT -p icmp --icmp-type echo-reply -j ACCEPT

✅ Make iptables Rules Persistent
bash
Copy
Edit
sudo apt install iptables-persistent
sudo netfilter-persistent save


📌 Summary
This project demonstrated how to prepare a secure and operational Linux system for remote management, while maintaining visibility and control over network diagnostics. These configurations are crucial in real-world SOC and admin scenarios where remote access and ping troubleshooting are part of the day-to-day responsibilities.

🧑‍💻 Author
Dipak Pakhrin
