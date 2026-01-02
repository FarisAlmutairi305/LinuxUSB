# Ubuntu Server Headless USB Reference

This USB contains **quick reference cheat sheets** for Ubuntu Server (headless) administration.  
All files are **Markdown** and safe to read — commands are **not executed automatically**.  

Use `nano`, `cat`, or `less` to read them directly from the USB.

---

## Included Cheat Sheets

| File | Description |
|------|-------------|
| `wifi.md` | Wi-Fi scanning, connecting, disconnecting, persistent connections, and troubleshooting |
| `Ethernet.md` | Wired network interface commands, temporary & persistent configuration (Netplan), troubleshooting |
| `usb.md` | Detecting, mounting, unmounting, and monitoring USB devices |
| `network_folder.md` | Discovering, connecting, creating, and mounting network shares (Samba/CIFS) |
| `services.md` | Managing systemd services: start, stop, restart, enable, disable, logs, listing, and configuration |
| `firewall.md` | UFW firewall: view rules, allow/deny ports/IPs/protocols, hardening, logging, and troubleshooting |
| `permissions.md` | File/folder permissions: viewing, changing, numeric/symbolic modes, special permissions, searching, ACLs |
| `system.md` | System info, uptime, processes, logs, updates, and performance monitoring |
| `files.md` | File/folder management, navigation, copying, moving, deleting, and searching |
| `packages.md` | Install, remove, update packages, search repositories, and manage software |
| `troubleshooting.md` | Common server troubleshooting commands for network, disk, services, and hardware |

---

## Usage Tips

- Open any cheat sheet in the terminal:
```
less wifi.md
nano wifi.md
cat wifi.md
```
- All commands require **sudo** if modifying system settings  
- Default configurations are safe to inspect; only execute commands you understand  
- Use `lsblk`, `ip link`, `ip addr`, and `systemctl` to check the current state before making changes  

---

## Recommended Reading Order

1. `Ethernet.md` / `wifi.md` – network connectivity first  
2. `usb.md` – managing storage devices  
3. `network_folder.md` – access network shares  
4. `services.md` – manage server services  
5. `firewall.md` – secure your server  
6. `permissions.md` – set correct file/folder access  
7. `packages.md` – install necessary software  
8. `files.md` – manage files and folders  
9. `system.md` – monitor and check system status  
10. `troubleshooting.md` – resolve issues  

---

## Notes

- Replace interface names (`wlan0`, `eth0`) and IPs with your actual configuration  
- Replace `<service_name>` with actual services like `ssh`, `nginx`, `apache2`  
- Commands are written for **Ubuntu Server (headless)**; some desktop tools are omitted  
- Keep this USB as a reference for **offline server administration**  

---
