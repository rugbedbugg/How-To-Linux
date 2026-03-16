# Git CLI Setup

Get `git` configured on a fresh machine so you can commit, sign, and use nicer tooling.

## 1. Set up basic configuration

Without these, you can't commit changes. Use `--global` so it applies to every repo — a bare
`git config user.name` only writes the *current* repo's config and errors out when you're not
inside a repo.
```bash
git config --global user.name <name>
git config --global user.email <email>
git config --global init.defaultBranch <default-branch-name>
```


## 2. Set up signed commits (personal preference)

I like the `Verified` badge on my commits on GitHub, so I sign them. There are two ways —
**SSH signing** (simplest, reuses your existing SSH key) or **GPG signing**.

### 2.1. SSH signing (recommended)

Reuses the SSH key you already authenticate with, so there's no separate key to manage.
```bash
git config --global gpg.format ssh
git config --global user.signingkey ~/.ssh/id_ed25519.pub
git config --global commit.gpgsign true
```
To verify your own signatures locally, add an allowed-signers file:
```bash
echo "<your-email> namespaces=\"git\" $(cat ~/.ssh/id_ed25519.pub)" >> ~/.ssh/allowed_signers
git config --global gpg.ssh.allowedSignersFile ~/.ssh/allowed_signers
```
You also have to upload the key to GitHub as a **signing** key (separate from the auth key):
```bash
gh ssh-key add ~/.ssh/id_ed25519.pub --type signing
```
See [SSH commit signing](../security/ssh-commit-signing.md) for the full walkthrough, including
the `admin:ssh_signing_key` scope gotcha.

### 2.2. GPG signing

```bash
git config --global commit.gpgsign true
git config --global user.signingkey <GPG-key-id>
```
If you don't have a GPG key yet, create one first with `gpg --full-generate-key`.


## 3. Use GitHub Desktop & lazygit

```bash
paru -S lazygit github-desktop-bin
```
These are graphical, but simpler to use and have a lower skill floor.
