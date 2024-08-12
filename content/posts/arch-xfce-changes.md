+++ 
date = 2024-06-20T00:43:03+01:00
title = "XFCE changes (Arch)"
description = ""
slug = ""
authors = []
tags = ["linux"]
categories = ["linux"]
externalLink = ""
series = []
+++

# Packages:

```bash
sudo pacman -S bluez bluez-utils arc-icon-theme arc-gtk-theme unzip fuse flameshot redshift copyq
```

# Keyboard shortcuts

- `super+w`: firefox
- `super+return`: terminal
- `super+i`: `xfce4-settings-manager`
- `print`: `flameshot gui`
- `shift+print`: `flameshot full --clipboard --path /home/user/Pictures/screenshots`
- `super+b`: `pkill -USR1 '^redshift$'`. [Setup reference](/posts/redshift/)
- `super`: `xfce4-popup-whiskermenu`. Requires [workaround](#super-key-workaround "jumps to super key workaround")

### Under Window Manager settings

- `super+d`: show desktop
- `super + left/right` to move windows (under window manager settings)

# Super key workaround

This example maps `Alt+F3` to `super` key. [Reference](https://www.reddit.com/r/xfce/comments/jr6y3s/problems_using_the_super_key_for_keyboard/)

- Install xcape.
- Add the following line to run on every startup: `xcape -e 'Super_L=Alt_L|F3'`
- Map `Alt+F3` to the shortcut you want to run with `super`

# Desktop

- Remove panel 2, bring panel 1 down.
- Add Whisker Menu, remove Applications Menu.

# Others

- Keyboard setting, repeat delay: 300, repeat speed: 30
- `mkdir -p ~/Pictures/screenshots ~/Documents ~/Music ~/Videos` (these folders don't exist, pin as bookmark too)
- Add to `.bashrc` file: `export EDITOR=nvim`
- Espanso official guide installs to `~/opt`, I prefer to keep everything in `/opt`
