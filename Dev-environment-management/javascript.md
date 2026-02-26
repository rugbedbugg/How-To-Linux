## [Option-1]: Setup system `nodejs` & `npm`

Install using system package manager
```bash
paru -S nodejs npm

# Update all system packages
paru -Syu
```

### Check version number
```bash
node -v
npm -v
```

## [Option-2]: Use `nvm`

Install Node Version Manager
```bash
paru -S nvm
```

Look for node versions to install and check for installed versions
```bash
nvm ls-remote
nvm list                # or, `nvm ls`
``` 

Install the preferred node versions to `nvm`
```bash
nvm install <version>
nvm install --lts       # install the latest version
```

### Set a version to be used

1. Only for the current terminal session
```bash
nvm user <version>
```

2. For all terminal sessions (set as default)
```bash
nvm alias default <version>
```

3. To use a specific version for a project
- Create a `.nvmrc` file in project root
```bash
echo "<version>" > .nvmrc
```

- Install and use the specified version
```bash
nvm install
nvm use
```

### Check version number
```bash
node -v
npm -v
```

## [Option-3]: Use `fnm` (Not compatible with `nvm`)

Install Fast Node Manager
```bash
paru -S fnm
```

Look for node versions to install and check for installed versions
```bash
fnm list-remote
fnm list
```

Install the preferred node versions to `fnm`
```bash
fnm install <version>
```

### Set a version to be used

1. Only for the current terminal session
```bash
fnm use <version>
```

2. For all terminal sessions (set as default)
```bash
fnm default <version>
```

3. To use a specific version for a project
- Create a `.nvmrc` or `.node-version` file in project root
```bash
echo "<version>" > .node-version
```

- Install the specified version
```bash
fnm install
```

### Auto-detect and set node version (as set in `.node-version` OR `.nvmrc`)
```bash
eval "$(fnm env --use-on-cd)"
```

### Check version number
```bash
node -v
npm -v
```
