# Firewall Commands (Ubuntu Server / UFW)

This file contains **commands to view, configure, and manage a firewall** on Ubuntu Server using UFW (Uncomplicated Firewall).  
Reference only — commands are **not executed automatically**.  
Works in terminal with nano, cat, or less.

---

## Check Current Firewall Status

View overall status:
```
sudo ufw status
```

View detailed status with rules and ports:
```
sudo ufw status verbose
```

Show numbered rules (for easy deletion):
```
sudo ufw status numbered
```

---

## Enable / Disable Firewall

Enable UFW:
```
sudo ufw enable
```

Disable UFW:
```
sudo ufw disable
```

Reset UFW to default (deletes all rules):
```
sudo ufw reset
```

---

## Default Policies

Set default **deny all incoming** (recommended for strong firewall):
```
sudo ufw default deny incoming
```

Set default **allow all outgoing** (recommended):
```
sudo ufw default allow outgoing
```

Set default **allow incoming** (less secure):
```
sudo ufw default allow incoming
```

Set default **deny outgoing** (rarely used):
```
sudo ufw default deny outgoing
```

---

## Allow or Deny Specific Ports

Allow a specific port (e.g., SSH 22):
```
sudo ufw allow 22
```

Allow a port with protocol (TCP or UDP):
```
sudo ufw allow 80/tcp
sudo ufw allow 53/udp
```

Deny a specific port:
```
sudo ufw deny 23
```

---

## Allow or Deny Specific IPs

Allow a specific IP:
```
sudo ufw allow from 192.168.1.50
```

Allow a specific IP to access a specific port:
```
sudo ufw allow from 192.168.1.50 to any port 22
```

Deny a specific IP:
```
sudo ufw deny from 192.168.1.100
```

---

## Allow or Deny Protocols

Allow a protocol (TCP or UDP):
```
sudo ufw allow proto tcp from any to any port 443
sudo ufw allow proto udp from any to any port 53
```

Deny a protocol:
```
sudo ufw deny proto tcp from any to any port 23
```

---

## Blocking Everything / Strong Firewall

Deny all incoming connections (strong firewall):
```
sudo ufw default deny incoming
```

Allow only specific ports/services (SSH, HTTP, HTTPS):
```
sudo ufw allow 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
```

Check status to ensure nothing else is allowed:
```
sudo ufw status verbose
```

Enable logging for audit:
```
sudo ufw logging on
```

---

## Check Firewall Rules and Strength

List numbered rules:
```
sudo ufw status numbered
```

Check if firewall blocks all unwanted traffic:
- Default deny incoming ✅  
- Only necessary ports open ✅  
- Only trusted IPs allowed ✅  
- Logging enabled ✅  

Audit with `sudo ufw status verbose` to find weaknesses.

---

## Deleting Rules

Delete a rule by port/protocol:
```
sudo ufw delete allow 80/tcp
```

Delete a rule by number:
```
sudo ufw status numbered
sudo ufw delete <rule_number>
```

---

## Advanced / Useful Tips

Allow a range of ports:
```
sudo ufw allow 1000:2000/tcp
```

Allow a subnet:
```
sudo ufw allow from 192.168.1.0/24
```

Enable rate limiting (protect against brute-force attacks):
```
sudo ufw limit 22/tcp
```

Check logs for blocked traffic:
```
sudo tail -f /var/log/ufw.log
```

---

## Notes

- UFW rules apply immediately when enabled  
- Always allow **SSH (22)** before enabling UFW on a server, otherwise you may lock yourself out  
- Default policy of **deny incoming / allow outgoing** is considered strong  
- Use `sudo ufw status verbose` to audit firewall rules  
- Use `less firewall.md` for easy viewing  

---
