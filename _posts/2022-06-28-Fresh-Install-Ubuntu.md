---
bg: "tools.jpg"
layout: post
title:  Fresh Install Ubuntu
crawlertitle: Fresh Install Ubuntu
summary: Fresh Install Ubuntu
date:   2022-06-28
categories: posts
tags: [linux]
author: jfdzar
---

In this post I will gather some tricks an things to do when installing Ubuntu Fresh, since recently I had to do it a couple of times

# Random Tricks

* For mounting drives and net drivers from fstab
```bash
sudo apt-get install cifs-utils
```
* Hide Mount Drives from the Dock
https://www.omgubuntu.co.uk/2019/11/hide-mounted-drives-ubuntu-dock
```bash
gsettings set org.gnome.shell.extensions.dash-to-dock show-mounts false
```

# Programs to install

* VS Code - Software Manager
* Dropbox - Software Manager
* GNOME Tweaks - Software Manager
* LTSpice - install wine and then install LTSPice.exe from their website - nothing special
* Hugo

```bash
sudo apt-get install curl
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

test -d ~/.linuxbrew && eval "$(~/.linuxbrew/bin/brew shellenv)"
test -d /home/linuxbrew/.linuxbrew && eval "$(/home/linuxbrew/.linuxbrew/bin/brew shellenv)"
test -r ~/.bash_profile && echo "eval \"\$($(brew --prefix)/bin/brew shellenv)\"" >> ~/.bash_profile
echo "eval \"\$($(brew --prefix)/bin/brew shellenv)\"" >> ~/.profile

brew install hugo

#Go to directory of the website
hugo serve -D
```
* Jekyll

```bash
sudo apt-get install ruby-full build-essential zlib1g-dev

echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

# Go to directory of the website
gem install jekyll bundler
bundle add webrick
bundle exec jekyll serve --trace
 
```

* Kicad


