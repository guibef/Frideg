---
layout: post
title: Shell Scripting 
subtitle: 
categories: Basics 
tags: [Shell, Bash]
---

## Create a Bash Script

### Create a file named `example.sh`

```
touch example.sh
```
By convention, bash script has a `.sh` file extension, but it works without it.

### Add shebang

Shell script starts with shebang `#!` following by the bash shell path.

For example, use `which bash` to find the path of bash shell, add `#! /usr/bin/bash` to `example.sh` and then add commands etc.

```sh
#! /usr/bin/bash 
echo "Hello World!"
```

### Make the script executable

```
chmod +x example.sh
```

### Run the script

```
$./hello.sh       
Hello World!
```
## Basic Syntax of Bash Scripting

### Variables

Define a variable with `foo=bar` and reference a variable with `$foo`.

### Numerical expressions

`$((expression))`, for example `var=$((1+2))`.

| Operator | Usage |
|------|------|
| `+` | addition |
| `-` | subtraction |
| `*` | multiplication |
| `/` | division |
| `**` | exponentiation |
| `%` | modulus |

### Numerical comparison

| Operation | Syntax |
|------|------|
| `a == b` | `a -eq b` |
| `a >= b` | `a -ge b` |
| `a > b`  | `a -gt b` |
| `a <= b` | `a -le b` |
| `a < b`  | `a -lt b` |
| `a != b` | `a -ne b` |

### Conditional statements

- `if ... then ... fi`
- `if ... then ... else ... fi`
- `if ... then ... elif ... then ... else ... fi`

```sh
if [[condition]]
then
    statement
elif [[condition]]
then
    statement
else
    statement
fi
```

### Looping

#### for loop

```sh
for i in {1..5}
do
    echo $i
done

for color in red yellow green
do
    echo $color
done
```

#### while loop

```sh
i=0
while [[ $i -le 10]]
do
    echo "$i"
    (( i += 1 ))
done
```

### Read user input

`read foo`, with a message `read -p "Enter your name" foo`.

### Read file

```sh
LINE=1

while read -r CURRENT_LINE
do
    echo "$LINE: $CURRENT_LINE"
    ((LINE++))
done < "my_file.txt"
```

### Execute commands

`||` **or** operator / `&&` **and** operator, can be used to conditionally execute commands based on exit codes.

`;`, commands can be separated in the same line with `;`.

#### Get the output of a command

`$(CMD)`, 
`<(CMD)`,
`` var=`CMD` ``

```sh
echo "Now is $(date)"

diff <(foo) <(bar)

var=`ls -a | grep foo`
echo $var
```

### Run with arguments

Run with `./example.sh arg1 arg2`

```sh
for i in $@
do
    echo "Entered arg is $i"
done
```

| Syntax | Meaning |
|------|------|
| `$0` | Name of the script |
| `$1` to `$9` | Arguments of the script, `$1` is the first argument etc.
| `$@` | All the arguments |
| `$#` | Number of arguments |
| `$?` | Return code of the previous command |
| `$$` | Process identification number (PID) for the current script |
| `!!` | Entire last command |
| `$_` | Last argument from the last command |

### Automate scripts via cron jobs

`* * * * *`, represents `minute/hour/day/month/weekday`

```sh
# cron job
* * * * * sh /path/to/example.sh
```
