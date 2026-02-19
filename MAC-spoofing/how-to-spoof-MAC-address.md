# NOTE
It is assumed here that  

## 1. Install `macchanger`
---
```bash
paru -S macchanger
```


## 2. Create a systemd service
---
systemd service file: `/etc/systemd/system/macspoof@.service`

```bash
[Unit]
Description=MAC Address Spoofing for %I
Wants=network-pre.target
Before=network-pre.target
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
Type=oneshot
ExecStart=/usr/bin/ip link set dev %I down
ExecStart=/usr/bin/macchanger -e %I
ExecStart=/usr/bin/ip link set dev %I up
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target

```
It is a `one-shot` service so it runs only once and is shown as active by `systemctl` even the process is done running after the first execute.

### Couple points to note:
- The `-e` flag preserves the 1st 3 bytes (vendor information) to prevent duplicate addresses within the same network
- The `-r` flag sets a completely random MAC address so it might suffer from the problem mentioned earlier.
- To reset back the permanent MAC address (your original MAC address), use the `-p` flag.
- These flags are not supposed to behave normally if they exist in the same command.


## 3. Stop NetworkManager from overriding
---
NetworkManager config file: `/etc/NetworkManager/NetworkManager.conf`

```bash
[device]
wifi.scan-rand-mac-address=no

[connection]
ethernet.cloned-mac-address=preserve
wifi.cloned-mac-address=preserve
```


## 4. Enable and start the service
---
```bash
sudo systemctl daemon-reload
sudo systemctl enable macspoof@wlan0.service
sudo systemctl start macspoof@wlan0.service
```


## 5. Verify that it works
---
```bash
macchanger --show wlan0
```
This should display your current MAC address (spoofed) and your permanent MAC address (original MAC address of the device).

If they are different, you're now spoofing your MAC address. Your MAC address will be randomized everytime you boot/reboot your device.


# Why should you spoof your MAC address
- Prevents tracking via your real MAC address on networks.
- Bypass/evade MAC-based Wi-Fi restrictions Ex:whitelists/blacklists in phone hotspots.
- Anonymity- Harder to identify and profile your device on public or monitored networks.

