# Creating Remote Repos from the Terminal

Two ways to get a local project onto GitHub: fully via `gh`, or with plain `git` + the web UI.

## 1. Install GitHub CLI (gh)

```bash
paru -S github-cli
```


## 2. Authenticate (one-time)

```bash
gh auth login
```
Choose:
- GitHub.com
- HTTPS/SSH (use SSH if you're a sigma)
- Authenticate via browser

Just follow the steps.


## 3. Create the repository

Create a repository from the terminal via `gh` or plain `git`.

### 3.1. gh (fully terminal workflow)
```bash
cd project-dir/
gh repo create
```
Follow the prompts and you'll have a remote repository on GitHub.

### 3.2. git (requires browser access)
```bash
cd project-dir/
git init
```
`git init` *initializes* version control in the current folder — it doesn't create a named repo
on GitHub. You'll make the remote on the website next.

### How to link this local repo to a remote on GitHub

- Go to [GitHub](https://github.com) and create an empty repo.
- Copy either the `https://….git` (HTTP) or `git@….git` (SSH) URL from the `Code` button.
- Back in the terminal, inside the repo, run:

### i. If the SSH url is used
```bash
# Add the remote. Use `add` the FIRST time — `set-url` only works if the remote already exists.
git remote add origin git@github.com:<username>/<repo-name>.git

# Push your branch and set it as the upstream (only needed on the first push).
git push -u origin <branch-name>

# Verify the remote is set
git remote -v
```
After that first `git push -u`, later pushes are just `git push`, and `git pull` brings down
changes from the remote.

### ii. If the HTTP url is used
```bash
git remote add origin https://github.com/<username>/<repo-name>.git
git push -u origin <branch-name>
git remote -v
```
