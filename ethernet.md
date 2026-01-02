# Ethernet & Wired Network Commands (Ubuntu Server)

This file contains **Ethernet and wired network commands** for headless Ubuntu Server.  
Reference only — commands are **not executed automatically**.  
Works in terminal with nano, cat, or less.

---

## Show Network Interfaces

List all interfaces:
```
ip link
```

Show IP addresses:
```
ip addr
```

Show only IPv4 addresses:
```
ip -4 addr
```

Show routing table:
```
ip route
```

Check default gateway:
```
ip route | grep default
```

---

## Configure Ethernet Interface Temporarily

Bring interface down:
```
sudo ip link set eth0 down
```

Bring interface up:
```
sudo ip link set eth0 up
```

Assign IP via DHCP:
```
sudo dhclient eth0
```

Assign static IP (temporary):
```
sudo ip addr add 192.168.1.100/24 dev eth0
sudo ip route add default via 192.168.1.1
```

Remove IP from interface:
```
sudo ip addr flush dev eth0
```

---

## Persistent Ethernet Configuration (Netplan)

Ubuntu Server uses **Netplan** for persistent network configuration.

1. Edit your Netplan YAML file:
```
sudo nano /etc/netplan/01-netcfg.yaml
```

2. Example static IP configuration:
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: no
      addresses:
        - 192.168.1.100/24
      gateway4: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8,8.8.4.4]
```

3. Example DHCP configuration:
```yaml
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: yes
```

4. Apply changes:
```
sudo netplan apply
```

---

## Test Connectivity

Ping another host or gateway:
```
ping -c 4 192.168.1.1
```

Ping external host (Internet):
```
ping -c 4 google.com
```

Check route to host:
```
traceroute google.com
```

Test open ports:
```
nc -zv 192.168.1.10 22
```

---

## Troubleshooting

Check link state and speed:
```
ethtool eth0
```

Check ARP table:
```
ip neigh
```

Check active connections:
```
ss -tunap
```

Release and renew DHCP lease:
```
sudo dhclient -r eth0
sudo dhclient eth0
```

Bring interface down/up if stuck:
```
sudo ip link set eth0 down
sudo ip link set eth0 up
```

---

## Notes

- Replace `eth0` with your actual Ethernet interface name (`ip link` to check)  
- Commands like `dhclient` require `sudo`  
- Persistent configuration should always be done via Netplan on Ubuntu Server  
- Use `less Ethernet.md` for easy viewing  

---
