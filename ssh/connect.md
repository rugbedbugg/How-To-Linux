# Connecting via SSH

Enable the SSH daemon and connect to a host (server or service) using your config aliases.

## 1. Enable and start the `sshd` service

```bash
sudo systemctl enable --now sshd
```


## 2. Check the `Host` alias of the service

Your SSH aliases live in `~/.ssh/config`. Instead of repeating the block here, see the annotated
example in [SSH Keys → Set nickname of ssh key](setup-keys.md#set-nickname-of-ssh-key-for-quick-access).

Each `Host` block maps a short alias (e.g. `dojo`) to a real `HostName` (e.g. `dojo.pwn.college`),
so you can type the alias instead of the full address.


## 3. Attempt to connect to the service

```bash
# Test the connection
ssh -T <Host/HostName>

# Actually connect to the service
ssh <Host/HostName>
```
NOTE:
- GitHub shows a "successfully authenticated" message but doesn't provide a shell.
- pwn.college provides a shell when there is an active challenge.
