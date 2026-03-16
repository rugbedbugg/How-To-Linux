# Encrypted Vault with gocryptfs

A password-locked folder that stays encrypted at rest and is only readable while "unlocked"
(mounted). Good for personal/sensitive files inside your home directory.

## 1. Install

```bash
paru -S gocryptfs        # or: pacman -S gocryptfs
```


## 2. How it works

Two directories:
```
~/vault/.cipher   # ciphertext — always encrypted, safe to back up anywhere
~/vault/open      # mountpoint — plaintext, ONLY while unlocked
```


## 3. Initialize (one time)

```bash
mkdir -p ~/vault/.cipher
gocryptfs -init ~/vault/.cipher
```
Pick a strong password and **save the printed master key** somewhere safe — it's your recovery
key if you forget the password.


## 4. Daily use

```bash
mkdir -p ~/vault/open
gocryptfs ~/vault/.cipher ~/vault/open   # unlock: prompts for the password
#   ... read/write sensitive files under ~/vault/open ...
fusermount3 -u ~/vault/open              # lock: encrypted at rest again
```

### Handy helper scripts
Drop these in `~/.local/bin` (make sure it's on your `PATH`):
```bash
# ~/.local/bin/vault-unlock
#!/usr/bin/env bash
mkdir -p "$HOME/vault/open"
mountpoint -q "$HOME/vault/open" || gocryptfs "$HOME/vault/.cipher" "$HOME/vault/open"

# ~/.local/bin/vault-lock
#!/usr/bin/env bash
mountpoint -q "$HOME/vault/open" && fusermount3 -u "$HOME/vault/open"
```
```bash
chmod +x ~/.local/bin/vault-unlock ~/.local/bin/vault-lock
```
Then just `vault-unlock` / `vault-lock`.


## 5. Notes
- Anything under `~/vault/.cipher` (the ciphertext) is safe to sync to cloud/USB as-is.
- This protects files *within* Linux. For whole-disk protection if the laptop is stolen, also use
  BitLocker (Windows) or LUKS (bare-metal Linux).
- For secrets you want to keep in git repos instead, see [git secrets](git-secrets.md).
