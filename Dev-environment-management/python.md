# Python Dev Environment Management

## 1. Setup a virtual environment [pre-existing project]
```bash
python -m venv <venv-name>
source <venv-name>/bin/activate

# If there is a requirements.txt file, install it
pip install -r requirements.txt
```

## 2. Setup a virtual environment a for fresh project

Create the new project using `uv`. Built using Rust and is faster that `pip`
```bash
uv init

# After following wizard create the virtual environment
uv venv

# Sync/Add/Remove dependencies
uv sync
uv add <dep-name>
uv remove <dep-name>

# Build the project
uv build

# Run the project
uv run main.py
```

## 3. Managing older python projects

There are often times where we are forced to run old python scripts which require an older version of python to run. In this case NEVER remove the system python and install an older one. We use a python version manager for this.

### 3.1. `uv` can handle this as well

```bash
# Locally install a different/older python version than the system python
uv python install <version-number>

# View available python versions to switch to for the curr. project
uv python list

# Switch to that version
uv python pin <version-number>
```

### 3.2. `pyenv` can also be used for the same purpose

1. Set the global python version (not recommended)
```bash
pyenv global <version-number>
```

2. Inside base directory of the repo, check if current python version and pyenv version match
```bash
pyenv versions
python --version
```

IF they DON'T MATCH
```bash
# Check where pyenv lives
# If it's `~/.pyenv`, Go ahead. If not, fix it first.
pyenv root
```

Run these commands to add `pyenv` to your environment path
```bash
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PYENV_ROOT/shims:$PATH"
eval "$(pyenv init -)"
source ~/.bashrc        # or ~/.zshrc
```

Now check if the python versions match
```bash
which python            # should show ~/.pyenv/shims/python
python --version
pynev versions
```

After both commands give the same output
```bash
# Check python version for the current directory
pyenv local

# If desired version is not installed
pyenv install <version-number>

# Set the desired python version as the project python interpreter
pyenv local <version-number>

# Check if version is set
python --version
```

