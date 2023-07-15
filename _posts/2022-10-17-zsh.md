---
layout: post
title: Zsh Terminal Autocompletion
subtitle: History based and Zsh-z autocompletion, user prompt customization
categories: Productivity
tags: [Terminal, Zsh, Shell, Config]
---

## Install Zsh
for Debian based distro

`sudo apt install zsh`

set Zsh as the default shell

`sudo chsh -s $(which zsh) ${USER}`

## Install [Zsh-z](https://github.com/agkozak/zsh-z) Plugin

```sh
mkdir -p ~/.zsh/plugins/zsh-z

curl https://raw.githubusercontent.com/agkozak/zsh-z/master/zsh-z.plugin.zsh \
-o ~/.zsh/plugins/zsh-z/zsh-z.plugin.sh
```

add `source ~/.zsh/plugins/zsh-z/zsh-z.plugin.sh` to `~/.zshrc`

## Zsh Config
save in `~/.zshrc`, use `source ~/.zshrc` to apply

```
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

# autocompletion using arrow keys
bindkey '^[OA' history-beginning-search-backward
bindkey '^[OB' history-beginning-search-forward

# PLUGINS

source ~/.zsh/plugins/zsh-z/zsh-z.plugin.sh

# Zsh-z plugin options
ZSH_CASE=smart # lower case patterns are treated as case insensitive
zstyle ':completion:*' menu select # improve completion menu style

# USER PROMPT
   
# enable command-subsitution in PS1
setopt PROMPT_SUBST
NL=$'\n'
PS1='$NL%B%F{cyan}%3~%f%b$NL%B%(?.%F{green}.%F{red})%(!.#.$)%f%b' 
```

## Autocompletion
check `man zshcomsys` for compinit

check `man zshoptions` and `man zshparam` for history setup

check `man zshzle` for bindkey, `ctrl + v` in terminal to find arrow keys' code, e.g. `^[OA` is up arrow and `^[OB` is down arrow in wsl2 Ubuntu and ChromeOS Debian; for Mac, it is `^[[A` and `^[[B`

## User Prompt
check `man zshmics` for prompt

### PS1 code
`%B (%b)`, boldface

`%F (%f)`, foreground color

`%3~`, current working directory, showing trailing `3`, replacing `$HOME` with `~`; `0` will show absolute path

`$NL`, new line, using variable `NL=$'\n'`

`%(?.%F{green}.%F{red})`, green if last command is success, red if error

`%(!.#.$)`, `#` if privilege, `$` is non-privilege