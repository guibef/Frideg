---
layout: post
title: Vim Setup and Basics
subtitle: 
categories: Productivity
tags: [Vim, Config]
---

Most contents of this post are from the [reference here](https://missing.csail.mit.edu/2020/editors/)

## Vim Config

Save the config to `~/.vimrc`

```
" Enable Vim functionality instead of 100% Vi compatibility
set nocompatible

" Turn of syntax highlighting
syntax on

" Highlight matching bracket
set showmatch

" Show line number
set number

" Enable relative line numbering mode
set relativenumber

" More powerful and intuitive backspacing
set backspace=indent,eol,start

" Set smart case sensitivity when searching
set ignorecase
set smartcase

" Enable searching while typing
set incsearch

" Always show the status line at the bottom
set laststatus=2
```

## Vim Basics

### Mode
- Normal: `<ESC>`
- Insert: `i`
- Replace: `r`
- Visual: `v`, line `V`, block `Ctrl-v`
- Command-line: `<ESC>` -> `:`

### Command-line
- `:q` quit
- `:w` save
- `:wq` save and quit

### Movement
- Basic movement: `hjkl` (left, down, up, right)
- Words: `w` (next word),`b` (beginning of word), `e` (end of word)
- Lines: `0` (beginning of line), `^` (first non-blank character), `$` (end of line)
- Screen: `H` (top of screen), `M` (middle of screen), `L` (bottom of screen)
- Scroll: `Ctrl-u `(up), `Ctrl-d` (down)
- File: `gg` (beginning of file), `G` (end of file)
- Line numbers: `:{number}<ENTER>` or `{number}G` (line {number})
- Misc: `%` (corresponding item)
- Find: `f{character}`, `t{character}`, `F{character}`, `T{character}`
    find/to forward/backward `{character}` on the current line, `,` / `;` for navigating matches
- Search: `/{regex}`, `n` / `N` for navigating matches

### Edit
- `i` insert
- `a` append
- `o` / `O` open line below / above
- `d{motion}` delete
- `c{motion}` change
- `x` delete character
- `s` substitute character
- `u` undo, `Ctrl-r` redo
- `y` copy, `p` paste
- `~` flip case

### Count
- `3w` move 3 words forward
- `5j` move 5 lines down
- `7dw` delete 7 words

### Modifier
- `ci(` change inside `()`
- `ca[` change around `[]`
- `di'` delete inside `''` 
