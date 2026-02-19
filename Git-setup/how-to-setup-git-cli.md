## 1. Setup up basic configuration

Without these, you can't commit changes.
```bash
git config user.name <name>
git config user.email <email>
git config init.defaultbranch <default-branch-name>
```


## 2. Set up signed commits (Personal Preference)

I like to have the `Verfied` badge on my commits on GitHub, so I have setup signed commits in git.
```bash
git config commit.gpgsign true
git config user.signingkey <GPG-key-value>
```
If you don't have a GPG key setup. Set it up first.


## 3. Use GitHub Desktop & lazygit

```bash
paru -S lazygit github-desktop-bin
```
These are graphical-based, but are simpler to use and have a lower skill ceiling.
