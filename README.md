# use_local_version_node

create in your project's root a file 
```
.nvmrc
```

In it, paste the version to be used
```
v16.14.2
```

ok, configuration created, go automatizated the change of glabal version for local version!
Your should use ZSH bash, in the .zshrc past the code

```
autoload -U add-zsh-hook
load-nvmrc() {
  local node_version="$(nvm version)"
  local nvmrc_path="$(nvm_find_nvmrc)"

  if [ -n "$nvmrc_path" ]; then
    local nvmrc_node_version=$(nvm version "$(cat "${nvmrc_path}")")

    if [ "$nvmrc_node_version" = "N/A" ]; then
      nvm install
    elif [ "$nvmrc_node_version" != "$node_version" ]; then
      nvm use
    fi
  elif [ "$node_version" != "$(nvm version default)" ]; then
    echo "Reverting to nvm default version"
    nvm use default
  fi
}
add-zsh-hook chpwd load-nvmrc
load-nvmrc
```

close Vscode and open it again and in the terminal it should show the changed version of nvm!!!
