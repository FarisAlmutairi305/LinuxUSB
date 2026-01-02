# USB Devices & Commands (Ubuntu Server)

This file contains **common commands to manage and inspect USB devices** on a headless Ubuntu Server.  
Reference only — commands are **not executed automatically**.  
Works in terminal with nano, cat, or less.

---

## List Connected USB Devices

Show all USB devices:
```
lsusb
```

Show detailed info about USB devices:
```
lsusb -v
```

Show kernel messages for USB devices:
```
dmesg | grep -i usb
```

---

## Show USB Storage Devices

List block devices (USB drives included):
```
lsblk
```

List detailed info with partitions:
```
sudo fdisk -l
```

Check device file for USB drive (e.g., /dev/sdb):
```
sudo blkid
```

---

## Mounting USB Drives

Create a mount point:
```
sudo mkdir -p /mnt/usb
```

Mount USB drive (example: /dev/sdb1):
```
sudo mount /dev/sdb1 /mnt/usb
```

Unmount USB drive:
```
sudo umount /mnt/usb
```

Mount with read/write options:
```
sudo mount -o rw /dev/sdb1 /mnt/usb
```

Check mounted filesystems:
```
df -h
```

---

## Troubleshooting USB Drives

Check kernel logs for errors:
```
dmesg | tail -n 50
```

Check USB drive health (requires `smartctl`):
```
sudo smartctl -a /dev/sdb
```

Repair filesystem (if needed):
```
sudo fsck /dev/sdb1
```

---

## Monitor USB Events in Real-Time

Monitor when a USB device is plugged or removed:
```
sudo dmesg -w
```

Use `udevadm` to monitor events:
```
sudo udevadm monitor --udev
```

---

## Notes

- Replace `/dev/sdb1` with your actual USB device file (`lsblk` to check)  
- Commands like `fdisk`, `mount`, and `fsck` require `sudo`  
- Always unmount before removing a USB drive to prevent data loss  
- Use `less usb.md` for easy viewing  

---
