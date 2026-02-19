## 1. Enable and start the sshd service
---
```bash
sudo systemctl enable --now sshd
```


## 2. Check the `HostName` or `Host` of the service
---
SSH config file: `~/.ssh/config`
```bash
# Main GitHub account
Host rugbedbugg
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_github
  IdentitiesOnly yes

# Second GitHub account
Host mystik-krysat
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_github_alt
  IdentitiesOnly yes

# pwn.college dojo
Host dojo
  HostName dojo.pwn.college
  User hacker
  IdentityFile ~/.ssh/id_ed25519_desktop
  IdentitiesOnly yes
```


## 3. Attempt to connect the service
---
```bash
# Test the connection
ssh -T <Host/HostName>

# Actually connect to the service
ssh <Host/HostName>
```
NOTE:
- Github will show connection successful but it doesn't provide a shell.
- pwn.college provides a shell when there is an active challenge.
