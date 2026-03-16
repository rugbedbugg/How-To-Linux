# Arch Linux on WSL2: First-Boot Setup

A fresh Arch WSL install drops you in as `root` with no `sudo` and no regular user. Fix that
before doing any real work.

## 1. Update the system & install essentials

```bash
pacman-key --init && pacman-key --populate archlinux
pacman -Syu --needed sudo git base-devel
```


## 2. Create a non-root user with sudo

```bash
# Create the user and add them to the 'wheel' group
useradd -m -G wheel -s /bin/bash <username>
passwd <username>            # set a password (needed for sudo)
```

Grant `sudo` to the `wheel` group:
```bash
# Writes a drop-in that's safer than editing /etc/sudoers directly
echo '%wheel ALL=(ALL:ALL) ALL' > /etc/sudoers.d/10-wheel
chmod 0440 /etc/sudoers.d/10-wheel
visudo -c                    # validate — should say "parsed OK"
```


## 3. Make that user the WSL default (and keep systemd)

Edit `/etc/wsl.conf`:
```ini
[boot]
systemd=true

[user]
default=<username>

[interop]
enabled=true
appendWindowsPath=true
```


## 4. Apply it

From **Windows** (PowerShell/CMD), restart the distro so `wsl.conf` takes effect:
```powershell
wsl --shutdown
```
Next launch, you'll come up as `<username>` with `systemd` running. Verify inside WSL:
```bash
whoami                       # -> <username>
systemctl is-system-running  # -> running (or degraded, both mean systemd is up)
```

## Next steps
- [Windows interop](windows-interop.md) — reach your Windows files from Arch.
- [SSH keys](../ssh/setup-keys.md) and [Git CLI setup](../git/setup-cli.md) to start committing.
