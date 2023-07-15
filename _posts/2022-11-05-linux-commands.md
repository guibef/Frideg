---
layout: post
title: Basic Linux Command
subtitle: 
categories: Basics 
tags: [Command, Shell]
---

## File and Navigating
`ls`, list, print the contents of the current directory

`.`, current directory

`..`, parent directory

`~`, home directory

`-`, previous directory

`/`, root

`cd`, change directory

`pwd`, print working directory

`mkdir`, make directory

`rm`, remove file

`rmdir`, remove directory

`cp`, copy

`mv`, move or rename

`touch`, update access date of a file or directory, if not existing, create one

## Read
`echo`, print out

`cat`, concatenate, read file and write to stdout

`more` or `less`, view file screen by screen

`grep`, global regular expression print, for searching

`diff`, show difference, `diff fileA fileB`

`find`, find files, eg. `find . -name '*.jpg' -exec mv {} ./jpg \;`

## Process
`ps`, process status, `aux` for all

`jobs`, status of jobs

`fg` / `bg`, foreground / background a process, `%` with job number

`&`, suffix to run in background

`ctrl-c`, SIGINT, stop process

`ctrl-\`, SIGQUIT, quit process

`kill -TERM <PID>`, SIGTERM, exit gracefully

`ctrl-z`, SIGTSTP, pause process

## Redirection
`|`, pipe output to input

`<`, redirect input

`>`, redirect output

`>>`, redirect output and append

## Programs
`sudo`, super user do

`which`, find path for a program

`date`, print date and time

`tee`, read input and write to stdout and file

`chmod`, change mode, permission

`man`, manual

`history`, shell history

## Environment Variable
`env` or `printenv`, print out environment variable

`$PATH`, path for programs

`$SHELL`, current shell

`$HOME`, home directory