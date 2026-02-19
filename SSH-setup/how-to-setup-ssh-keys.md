## 1. Generate keys

```bash
ssh-keygen 
```
- Make a note of where the key will be stored. (1st prompt)
- Go through the setup
- Use default options if not sure. 
- For a casual user, the time to expire can be set to `never`


## 2. List the keys

```bash
# Default directory for storing SSH keys
ls ~/.ssh/


# If you want to delete a key
# 1. Make sure they're not loaded into the ssh-agent
ssh-add -l

# 2. Remove the key to be deleted, from the agent
#   - The agent always contains the private key
#   - The .pub public key is provided to the online service
#   - Delete the public key from the website
# Remove the private key like so: 
ssh-add -d ~/.ssh/<key-name>

# 3. Now delete both the public and private keys from the system
rm ~/.ssh/<key-name>
rm ~/.ssh/<key-name>.pub
```
- SSH keys are used to provide secure, passwordless authentication for remote access to systems over unsecured networks.
- They replace traditional password-based login methods, which are vulnerable to brute-force attacks, credential theft, and replay attacks.


## 3. How to use the keys

First print out the public key:
```bash
cat ~/.ssh/<key-name>.pub
```
Supply the entire output of this command to the online service you're trying to connect to.

Next add the corresponding private key (the one w/o a file extension) to the `ssh-agent`

3.1. Make sure the agent is running.
```bash
eval "$(ssh-agent -s)"
```
3.2. Check if multiple agent processes are running.
```bash
pgrep ssh-agent
```
If yes, kill all processes. Run only one process.
```bash
pkill ssh-agent && eval "$(ssh-agent -s)"
pgrep ssh-agent
```
3.3. Add the private key to the agent
The private key doesn't have a file extension.
```bash
ssh-add ~/.ssh/<key-name>
```
3.4. List the added keys and check if it's added
```bash
ssh-add -l
```

### Set nickname of ssh key for quick access
SSH key config file: `~/.ssh/config`
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
Here, pwn.college is a good example. Instead of connecting using `dojo.pwn.college` we can use `dojo` as an alias.
