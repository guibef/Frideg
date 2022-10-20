---
layout: post
title: Zsh Terminal Autocompletion
subtitle: History based and Zsh-z
categories: Productivity
tags: [Terminal, Zsh]
---

## Install Zsh
for Debian based distro

`sudo apt install zsh`

set zsh as the default shell

`sudo chsh -s $(which zsh) ${USER}`

## Zsh Config
save in `~/.zshrc`, use `source ~/.zshrc` to apply

```
# PREFERENCE

# enable vi mode
bindkey -v 

# AUTOCOMPLETION

# initialize autocompletion
autoload -Uz compinit && compinit

# history setup
setopt APPEND_HISTORY
setopt SHARE_HISTORY
setopt EXTENDED_HISTORY
setopt HIST_EXPIRE_DUPS_FIRST
HISTFILE=$HOME/.zhistory
SAVEHIST=1000
HISTSIZE=999

# autocompletion using arrow keys (based on history)
bindkey '^[OA' history-beginning-search-backward
bindkey '^[OB' history-beginning-search-forward

# USER PROMPT
   
# enable command-subsitution in PS1
setopt PROMPT_SUBST
NL=$'\n'
PS1='$NL%B%F{cyan}%3~%f%b$NL%B%(?.%F{green}.%F{red})%(!.#.$)%f%b' 

# PLUGINS

source ~/.zsh/plugins/zsh-z/zsh-z.plugin.sh

# Zsh-z plugin options
ZSH_CASE=smart # lower case patterns are treated as case insensitive
zstyle ':completion:*' menu select # improve completion menu style
```

## Autocompletion
check `man zshcomsys` for compinit

check `man zshoptions` and `man zshparam` for history setup

check `man zshzle` for bindkey, `ctrl + v` in terminal to find arrow keys' code, e.g. `^[OA` is up arrow and `^[OB` is down arrow in wsl2 Ubuntu and ChromeOS Debian

## User Prompt
check `man zshmics` for prompt

### PS1 code
`%B (%b)`, boldface

`%F (%f)`, foreground color

`%3~`, current working directory, showing trailing `3`, replacing `$HOME` with `~`; `0` will show absolute path

`$NL`, new line, using variable `NL=$'\n'`

`%(?.%F{green}.%F{red})`, green if last command is success, red if error

`%(!.#.$)`, `#` if privilege, `$` is non-privilege

## Plugins
### Zsh-z
install

```sh
mkdir -p ~/.zsh/plugins/zsh-z

curl https://raw.githubusercontent.com/agkozak/zsh-z/master/zsh-z.plugin.zsh \
-o ~/.zsh/plugins/zsh-z/zsh-z.plugin.sh
```

add `source ~/.zsh/plugins/zsh-z/zsh-z.plugin.sh` to `~/.zshrc`
