# Network Folders & Samba (Ubuntu Server)

This file contains **commands to discover, access, create, and mount network folders (Samba/CIFS shares)** on Ubuntu Server.  
Reference only — commands are **not executed automatically**.  
Works in terminal with nano, cat, or less.

---

## Discover Network Shares

List shares on a specific IP (requires `smbclient`):
```
smbclient -L //192.168.1.100 -U username
```

Scan the network for available hosts:
```
nmap -p 139,445 192.168.1.0/24
```

Check connectivity to a host:
```
ping -c 4 192.168.1.100
```

---

## Connect to a Network Share

Temporary connection (interactive):
```
smbclient //192.168.1.100/share -U username
```

List files on the share:
```
ls
```

Download a file:
```
get filename
```

Upload a file:
```
put filename
```

---

## Create a Network Share (Samba Server)

Install Samba server:
```
sudo apt update
sudo apt install samba
```

Create a folder to share:
```
sudo mkdir -p /srv/samba/share
sudo chmod 2770 /srv/samba/share
sudo chown nobody:nogroup /srv/samba/share
```

Edit Samba configuration:
```
sudo nano /etc/samba/smb.conf
```

Add a section like:
```
[share]
   path = /srv/samba/share
   browseable = yes
   read only = no
   guest ok = yes
```

Restart Samba:
```
sudo systemctl restart smbd
sudo systemctl enable smbd
```

---

## Mount a Network Folder (CIFS/SMB)

Install cifs-utils if not already installed:
```
sudo apt install cifs-utils
```

Create a mount point:
```
sudo mkdir -p /mnt/network_share
```

Mount the network share (temporary):
```
sudo mount -t cifs //192.168.1.100/share /mnt/network_share -o username=username,password=PASSWORD
```

Mount read-only:
```
sudo mount -t cifs //192.168.1.100/share /mnt/network_share -o ro,username=username,password=PASSWORD
```

Unmount the share:
```
sudo umount /mnt/network_share
```

---

## Persistent Mount (fstab)

Edit `/etc/fstab` to auto-mount at boot:
```
sudo nano /etc/fstab
```

Add a line like:
```
//192.168.1.100/share /mnt/network_share cifs username=username,password=PASSWORD,iocharset=utf8,uid=1000,gid=1000 0 0
```

Test fstab mount without reboot:
```
sudo mount -a
```

---

## Troubleshooting

Check if the share is reachable:
```
smbclient -L //192.168.1.100 -U username
```

Check mount status:
```
mount | grep network_share
```

Check logs if Samba server issue:
```
sudo journalctl -u smbd
```

Check for blocked ports (139, 445):
```
sudo ufw status
sudo iptables -L
```

---

## Notes

- Replace `192.168.1.100` with the target host IP  
- Replace `username`, `PASSWORD`, and `share` with actual credentials and share names  
- Use `sudo` when creating shares, mounting, or editing Samba config  
- Use `less network_folder.md` for best viewing  

---
