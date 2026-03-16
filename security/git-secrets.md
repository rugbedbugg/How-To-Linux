# Keeping Secrets Out of Git Repos

Never push API keys, `.env` files, or private keys in plaintext. Three layers, from safety net to
full encryption.

## 0. Safety net: a global gitignore

Block common secret patterns everywhere, so you can't commit them by accident:
```bash
git config --global core.excludesFile ~/.config/git/ignore
mkdir -p ~/.config/git
cat >> ~/.config/git/ignore <<'EOF'
*.pem
*.key
*.env
.env
.env.*
!.env.example
id_rsa
id_ed25519
*.kdbx
secrets.yaml
.secrets/
EOF
```
This *hides* secrets from git but doesn't encrypt anything — it's the last line of defense, not
the plan.


## Option A: git-crypt (transparent whole-file encryption)

Files matching a pattern are auto-encrypted on commit, auto-decrypted on checkout. Great for
whole secret files.

```bash
paru -S git-crypt

cd your-repo/
git-crypt init

# Mark which files to encrypt, in .gitattributes:
cat > .gitattributes <<'EOF'
secrets/**   filter=git-crypt diff=git-crypt
*.env        filter=git-crypt diff=git-crypt
*.key        filter=git-crypt diff=git-crypt
EOF

# Back up the repo key (store it OUTSIDE the repo, e.g. in your vault):
git-crypt export-key ~/vault/open/<repo>.key
```
Without that exported key you can't decrypt the files on another machine.


## Option B: SOPS + age (encrypt values, diff-friendly)

Encrypts *values* inside YAML/JSON/env files while leaving keys readable, so diffs stay
meaningful. Better for structured config.

```bash
paru -S sops age

# One-time: create an age key
mkdir -p ~/.config/sops/age
age-keygen -o ~/.config/sops/age/keys.txt
# note the public key it prints: age1........
```

Per repo, add `.sops.yaml`:
```yaml
creation_rules:
  - path_regex: (secrets|\.env).*
    age: age1xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
```
Then:
```bash
sops -e -i secrets.yaml    # encrypt in place
sops secrets.yaml          # open decrypted in your editor; re-encrypts on save
```


## Which one?
| Need | Use |
|------|-----|
| Encrypt whole files (keys, certs, dumps) | **git-crypt** |
| Encrypt values in config, keep readable diffs | **SOPS + age** |
| Just don't want to *accidentally* commit | the global **gitignore** above |

For secrets you keep locally rather than in a repo, see the
[gocryptfs vault](encrypted-vault-gocryptfs.md).
