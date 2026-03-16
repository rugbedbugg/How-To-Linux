# How-To-Linux

My personal, no-fluff how-to notes for setting up and running a Linux box — the stuff I'd
otherwise re-google every few months. Written as terminal-first cheatsheets.

> **Assumptions:** these guides target **Arch Linux**. `paru` is an AUR helper (swap for `yay`,
> or use plain `pacman` for official-repo packages). Commands that touch hardware (e.g. Wi-Fi
> interface names) may need tweaking for your machine.

## Contents

### Git
- [Git CLI setup](git/setup-cli.md) — identity, signed commits (SSH & GPG), GUI tools
- [Creating remote repos from the terminal](git/create-remote-repos.md) — `gh` and plain-`git` workflows

### SSH
- [SSH keys: setup & management](ssh/setup-keys.md) — generate, list, delete, use, config aliases
- [Connecting via SSH](ssh/connect.md) — the `sshd` service and connecting by alias

### Dev environments
- [Python](dev-environments/python.md) — `venv`, `uv`, and `pyenv` version management
- [JavaScript / Node](dev-environments/javascript.md) — system Node, `nvm`, and `fnm`

### WSL (Arch on Windows)
- [Arch on WSL2: first-boot setup](wsl/setup-arch-wsl.md) — sudo user, `wheel`, `wsl.conf`, systemd
- [Windows interop](wsl/windows-interop.md) — drives, symlinks, `explorer.exe`, the `/mnt/c` speed trap

### Security
- [SSH commit signing](security/ssh-commit-signing.md) — the GitHub Verified badge, and the scope gotcha
- [Encrypted vault (gocryptfs)](security/encrypted-vault-gocryptfs.md) — a password-locked folder
- [Keeping secrets out of git](security/git-secrets.md) — global gitignore, git-crypt, SOPS + age

### Networking / privacy
- [MAC address spoofing](mac-spoofing/spoof-mac-address.md) — randomize your MAC on every boot

## License

[MIT](LICENSE) — use freely, no warranty.
