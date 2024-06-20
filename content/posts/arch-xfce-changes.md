+++ 
date = 2024-06-20T00:43:03+01:00
title = "XFCE changes (Arch)"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

# Packages:

`sudo pacman -S bluez arc-icon-theme arc-gtk-theme unzip fuse flameshot redshift`

# Keyboard shortcuts

- `super+w`: firefox
- `super+return`: terminal
- `super+i`: `xfce4-settings-manager`
- `alt-d`: show desktop
- `super + left/right` to move windows (under window manager settings)
- `print`: `flameshot gui`
- `shift+print`: `flameshot full --clipboard --path /home/user/Pictures/screenshots`

# Desktop

- remove panel 2, bring panel 1 down
- Add Whisker Menu, remove Applications Menu

# Others

- Keyboard setting, repeat delay: 300, repeat speed: 30
- `mkdir -p ~/Pictures/screenshots ~/Documents ~/Music ~/Videos` (these folders don't exist)
- Add to `.bashrc` file: `export EDITOR=nvim`
- espanso official guide installs it to ~/opt , for me just install to /opt

# To fix

- Fix super hotkey bug.
- toggle redshift with 1 hotkey.
