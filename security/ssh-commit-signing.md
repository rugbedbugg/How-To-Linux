# SSH Commit Signing (the Verified badge)

Sign your git commits with your existing SSH key so GitHub shows the **Verified** badge — no
separate GPG key to manage.

## 1. Point git at your SSH key for signing

```bash
git config --global gpg.format ssh
git config --global user.signingkey ~/.ssh/id_ed25519.pub
git config --global commit.gpgsign true
git config --global tag.gpgsign true
```


## 2. Let git verify your own signatures locally

```bash
echo "<your-email> namespaces=\"git\" $(cat ~/.ssh/id_ed25519.pub)" >> ~/.ssh/allowed_signers
git config --global gpg.ssh.allowedSignersFile ~/.ssh/allowed_signers
```


## 3. Upload the key to GitHub as a SIGNING key

A key added for **authentication** is *not* automatically a **signing** key — they're separate on
GitHub. If you only ran `gh auth login`, you have the auth key but not the signing one.

```bash
gh ssh-key add ~/.ssh/id_ed25519.pub --title "signing key" --type signing
```

### Gotcha: the scope error
If you see:
```
HTTP 404 ... This API operation needs the "admin:ssh_signing_key" scope.
```
your `gh` token lacks the scope. Grant it, then retry:
```bash
gh auth refresh -h github.com -s admin:ssh_signing_key
gh ssh-key add ~/.ssh/id_ed25519.pub --title "signing key" --type signing
```


## 4. Verify

```bash
git commit --allow-empty -m "signed test"
git log --show-signature -1
```
You want to see **`Good "git" signature for <your-email>`**. Once the signing key is on GitHub,
pushed commits show the **Verified** badge.

See also: [Git CLI setup](../git/setup-cli.md) for the GPG alternative.
