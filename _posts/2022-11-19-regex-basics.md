---
layout: post
title: Regular Expression (Regex) 
subtitle: 
categories: Basics 
tags: [Regex]
---

## Basic

### Anchors

`^abc`, start with **abc**

`abc$`, end with **abc**

`^abc$`, exact match **abc**

### Quantifiers

`c*`, zero or more **c**

`(ab)*`, zero or more **ab** and capture it

`c+`, one or more **c**

`c?`, zero or one **c**

`c{2}`, 2 **c**

`c{2,}`, 2 or more **c**

`c{2, 4}`, 2 to 4 **c**

### OR operator

`(a|b)`, **a** or **b**, and capture it

`[ab]`, **a** or **b**, without capturing it

### Characters

`\d`, a digit char

`\w`, a word char, alphanumeric + underscore

`\s`, a whiter space char

`.`, any chars 


`\D`, `\W`, `\S`, inverse match respectively

`\`, escape chars `^.[$()|*+?{\`

### Flags

`g`, global

`m`, multi-line

`i`, case-insensitive

## Intermediate

### Grouping and Capturing

`(ab)`, a capturing group **ab**

`(?:ab)`, disable the capturing group

`(?<foo>bc)`, name the capturing group **foo**

### Bracket

`[a-z]`, a lower case letter

`[0-9]`, a single decimal digit number

`[a-fA-F0-9]`, a single hexadecimal digit, case insensitive

`[^a-zA-Z]`, not a letter, `^` is negation inside `[]`

### Greedy and Lazy Match

`*`, `+`, `{}`, greedy operators

`?`, can be used to make it lazy

## Advance

### Boundary

`\babc`, **abc** begin on a word boundary 

`abc\b`, **abc** end on a word boundary 

`\babc\b`, exact word **abc**

`\Babc`, **abc** not begin on a word boundary

`abc\B`, **abc** not end on a word boundary

`\Babc\B`, **abc** not begin and end on a word boundary

### Back-references

`([abc])([def])\2\1`, `\1` or `\2` matches the first or second captured group

`(?<foo>[abc])\k<foo>`, `\k<foo>` match the captured group named **foo**

### Look-ahead and Look-behind

`a(?=b)`, **a** that is followed by **b**

`(?<=b)a`, **a** that is preceded by **b**

`a(?!b)`, **a** that is not followed by **b**

`(?!b)a`, **a** that is not preceded by **b**