# Services & Systemd Commands (Ubuntu Server)

This file contains **commands to manage and inspect services** on Ubuntu Server using systemd.  
Reference only — commands are **not executed automatically**.  
Works in terminal with nano, cat, or less.

---

## Start / Stop / Restart Services

Start a service:
```
sudo systemctl start <service_name>
```

Stop a service:
```
sudo systemctl stop <service_name>
```

Restart a service:
```
sudo systemctl restart <service_name>
```

Reload service configuration without stopping:
```
sudo systemctl reload <service_name>
```

---

## Enable / Disable Services

Enable service to start at boot:
```
sudo systemctl enable <service_name>
```

Disable service from starting at boot:
```
sudo systemctl disable <service_name>
```

Check if a service is enabled:
```
sudo systemctl is-enabled <service_name>
```

---

## View Service Status & Details

Check the status of a service:
```
sudo systemctl status <service_name>
```

Show detailed information about a service:
```
sudo systemctl show <service_name>
```

View the journal logs for a service:
```
sudo journalctl -u <service_name>
```

View real-time logs for a service:
```
sudo journalctl -f -u <service_name>
```

---

## List Services

List all active/running services:
```
systemctl list-units --type=service --state=running
```

List all loaded services (active, inactive, failed):
```
systemctl list-units --type=service --all
```

List all installed service unit files:
```
systemctl list-unit-files --type=service
```

---

## Inspect Service Startup Behavior

Check how a service is started (systemd unit type, dependencies):
```
systemctl cat <service_name>
```

Show dependencies of a service:
```
systemctl list-dependencies <service_name>
```

Check which services start at boot:
```
systemctl list-unit-files | grep enabled
```

Check which services are currently running at boot:
```
systemctl list-units --type=service --state=running
```

---

## Modify Service Configuration

Edit a service configuration override (safe way):
```
sudo systemctl edit <service_name>
```

Reload systemd after changing unit files:
```
sudo systemctl daemon-reload
```

Restart service to apply changes:
```
sudo systemctl restart <service_name>
```

---

## Useful Tips

- Replace `<service_name>` with the actual service (e.g., `ssh`, `apache2`, `nginx`)  
- Always check `status` and `journalctl` after changes  
- Use `enable` and `disable` to control persistent startup  
- Use `systemctl cat` to inspect the exact configuration used  
- Use `systemctl list-unit-files --type=service` to audit installed services  

---
