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
- HTTPS/SSH (Use SSH if you're a sigma)
- Authenticate via browser 

Just follow the steps.


## 3. Create the repository

Create a repository from the terminal via git/gh

## 3.1. gh (Fully terminal workflow)
```bash
cd project-dir/
gh repo create
```
Just follow the steps and you'll have a remote repository on GitHub.

## 3.2. git (Requires browser access)
```bash
cd project-dir/
git init
```
And a repo with the name `project-dir` will be created locally. 

### How to have this local repo as a remote repo in GitHub

- Goto [Github](https://github.com) to create a repo.
- Copy the `https:// ... .git` url available via the `Code` button
- Come back into the terminal and inside the repository, run:

### i. If SSH url used
```bash
git remote set-url <your-remote-name> git@github.com:<username>/<repo-name>.git
git push -u <your-remote-name> <branch-to-set-upstream-to>

# Check if the remote is set
git remote -v

# The previous `git push` command is the only time 
# you'd need to run that in this repo
# After the first time, run
git pull
```

### ii. If HTTP url used
```bash
git remote set-url <your-remote-name> https://github.com/<username>/<repo-name>.git
git push -u <your-remote-name> <branch-to-set-upstream-to>

# Check if the remote is set
git remote -v

# The previous `git push` command is the only time 
# you'd need to run that in this repo
# After the first time, run
git pull
```
