# How-To-Linux

My personal, no-fluff how-to notes for setting up and running a Linux box — the stuff I'd
otherwise re-google every few months. Written as terminal-first cheatsheets.

> **Assumptions:** these guides target **Arch Linux**. `paru` is an AUR helper (swap for `yay`,
> or use plain `pacman` for official-repo packages). Commands that touch hardware (e.g. Wi-Fi
> interface names) may need tweaking for your machine.

## Contents

### Git
- [Git CLI setup](git/setup-cli.md)
- [Creating remote repos from the terminal](git/create-remote-repos.md)

### SSH
- [SSH keys: setup & management](ssh/setup-keys.md)
- [Connecting via SSH](ssh/connect.md)

### Dev environments
- [Python](dev-environments/python.md)
- [JavaScript / Node](dev-environments/javascript.md)

### WSL (Arch on Windows)
- [Arch on WSL2: first-boot setup](wsl/setup-arch-wsl.md)
- [Windows interop](wsl/windows-interop.md)

### Security
- [SSH commit signing](security/ssh-commit-signing.md)
- [Encrypted vault (gocryptfs)](security/encrypted-vault-gocryptfs.md)
- [Keeping secrets out of git](security/git-secrets.md)

### Networking / privacy
- [MAC address spoofing](mac-spoofing/spoof-mac-address.md)

## License

[MIT](LICENSE)
