# WSL ↔ Windows Interop

How to reach your Windows files from Arch, run Windows programs, and avoid the classic
performance trap.

## 1. Windows drives from Arch

Your drives are auto-mounted under `/mnt`:
```bash
/mnt/c/...    # C: drive  (e.g. /mnt/c/Users/<you>/Downloads)
/mnt/d/...    # D: drive
```

A tidy way to keep shortcuts is a folder of symlinks:
```bash
mkdir -p ~/Windows
ln -sfn /mnt/c ~/Windows/C
ln -sfn /mnt/d ~/Windows/D
# now:  cd ~/Windows/C/Users/<you>
```


## 2. Arch files from Windows

Browse your Linux home from Explorer or any Windows app via:
```
\\wsl.localhost\archlinux\home\<username>
```


## 3. Run Windows programs from Arch

```bash
explorer.exe .            # open the current Arch folder in Windows Explorer
clip.exe < file.txt       # pipe Arch output into the Windows clipboard
powershell.exe -c "..."   # run a PowerShell one-liner
```

### Open URLs in the Windows browser
Plain Arch has no `xdg-open` handler for a Windows browser, so tools like `gh` can't open a login
page. Drop in a tiny shim:
```bash
sudo tee /usr/local/bin/wslview >/dev/null <<'EOF'
#!/usr/bin/env bash
explorer.exe "$@" >/dev/null 2>&1 || true
exit 0
EOF
sudo chmod +x /usr/local/bin/wslview
echo 'export BROWSER=wslview' | sudo tee /etc/profile.d/wsl-browser.sh
```
(`wslu` from the AUR provides a fuller `wslview`, but this shim is enough for `gh`, `xdg-open`, etc.)


## ⚠️ 4. Keep active repos in the Linux filesystem, NOT `/mnt/c`

This is the one rule that matters for dev work:

- **Speed** — cross-filesystem access to `/mnt/c` is *much* slower. `git status`, `npm install`,
  and builds can be 10–50× slower there than in `~`.
- **Permissions** — `/mnt/c` can't store Linux file modes, so `chmod` won't stick (bad for SSH
  keys) and file-mode noise dirties git diffs.

So: **clone and build projects in `~`** (e.g. `~/Projects/...`); only reach into `~/Windows/...`
when you need to grab or drop a Windows file.
