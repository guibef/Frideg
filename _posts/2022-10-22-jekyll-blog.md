---
layout: post
title: How to Build a Blog Site
subtitle: Using Jekyll and Yat Theme
categories: Tutorials
tags: [Jekyll, Blog]
---

Instructions are based on ChromeOS Debian Linux

## Install [Jekyll](https://jekyllrb.com/docs/)

### Install Ruby and other prerequisites

`sudo apt install ruby-full build-essential zlib1g-dev`

### Add environment variables to configuration file

Add below to `~/.zshrc`

```
# Install Ruby Gems to ~/gems
export GEM_HOME="$HOME/gems"
export PATH="$HOME/gems/bin:$PATH"
```
`source ~/.zshrc` to apply

### Install Jekyll and Bundler

`gem install jekyll bundler`

## Clone a [Jekyll Theme](https://jekyllrb.com/docs/themes/) 

Use a theme as a starting point, for example [Yat Theme](https://github.com/jeffreytse/jekyll-theme-yat) which is what this blog site is built upon

Understand the basics about Jekyll site following this [step by step tutorial](https://jekyllrb.com/docs/step-by-step/01-setup/)

## Build Jekyll Site Locally

### Build and run

in the Jekyll site root directory, run

`bundle install`

`bundle exec jekyll serve`

### Test locally

browse to [localhost:4000](http://localhost:4000)

## Customize the Jekyll Theme

start from the `_config.yml`, then add markdown files to `_posts`

