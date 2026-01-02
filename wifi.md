# Wi-Fi Commands (Ubuntu Server Headless)

This file contains **Wi-Fi commands for headless Ubuntu Server**.  
Reference only — commands are **not executed automatically**.  
Works in terminal with nano, cat, or less.

---

## Show Wi-Fi Devices & Interfaces

List wireless devices:
```
iw dev
```

Show wireless interface details:
```
iwconfig
```

List interface names:
```
ip link
```

Check current IP addresses:
```
ip addr show
```

---

## Scan for Wi-Fi Networks

Scan all nearby Wi-Fi networks:
```
sudo iw dev wlan0 scan | grep SSID
```

Show channels and frequencies:
```
iwlist wlan0 channel
```

Check signal strength of current connection:
```
iwconfig wlan0
```

---

## Connect to Wi-Fi (wpa_supplicant)

### Temporary Connection (for current session)
1. Create a temporary configuration file:
```
sudo wpa_passphrase "SSID" "PASSWORD" | sudo tee /etc/wpa_supplicant.conf
```

2. Start wpa_supplicant:
```
sudo wpa_supplicant -B -i wlan0 -c /etc/wpa_supplicant.conf
```

3. Get an IP address:
```
sudo dhclient wlan0
```

4. Check connection:
```
iw dev wlan0 link
ip addr show wlan0
```

---

## Disconnect from Wi-Fi

Stop wpa_supplicant:
```
sudo pkill wpa_supplicant
```

Release IP:
```
sudo dhclient -r wlan0
```

Bring interface down:
```
sudo ip link set wlan0 down
```

Bring interface up:
```
sudo ip link set wlan0 up
```

---

## Make Wi-Fi Connection Persistent

1. Edit `/etc/wpa_supplicant/wpa_supplicant.conf` to include your network(s):
```
network={
    ssid="SSID"
    psk="PASSWORD"
}
```

2. Enable systemd service for your interface:
```
sudo systemctl enable wpa_supplicant@wlan0
sudo systemctl start wpa_supplicant@wlan0
```

3. Assign IP automatically via DHCP:
```
sudo dhclient wlan0
```

After reboot, Wi-Fi will connect automatically.

---

## Troubleshooting

Check current link and signal:
```
iw dev wlan0 link
iwconfig wlan0
```

Check IP addresses:
```
ip addr show wlan0
```

Release and renew IP if needed:
```
sudo dhclient -r wlan0
sudo dhclient wlan0
```

Check interface stats:
```
iw dev wlan0 station dump
```

---

## Notes

- Replace `wlan0` with your actual Wi-Fi interface name (`ip link` to check)  
- Commands require `sudo`  
- No desktop tools (`nmcli`) are needed  
- Use `less wifi.md` for best viewing  

---
