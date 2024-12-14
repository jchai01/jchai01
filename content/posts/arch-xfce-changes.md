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

`sudo pacman -S --needed base-devel git network-manager-applet thunar-archive-plugin wget bluez bluez-utils arc-icon-theme arc-gtk-theme unzip fuse flameshot redshift copyq tmux neovim libreoffice mpv xcape net-tools`

- network-manager-applet - in order to see the network icon in XFCE.
- thunar-archive-plugin - right click extract feature.

# Keyboard shortcuts

- `super+w`: firefox
- `super+return`: terminal
- `super+i`: `xfce4-settings-manager`
- `print`: `flameshot gui`
- `shift+print`: `flameshot full --clipboard --path /home/user/Pictures/screenshots`
- `super+b`: `pkill -USR1 '^redshift$'`. [Setup reference](/posts/redshift/)
- `Alt+F3`: `xfce4-popup-whiskermenu`. Maps to `super` eventually, see [super key workaround](#super-key-workaround "jumps to super key workaround")

### Under Window Manager settings

- `super + left/right` to move windows (under window manager settings)

# Super key workaround

This example maps `Alt+F3` to `super` key. [Reference](https://www.reddit.com/r/xfce/comments/jr6y3s/problems_using_the_super_key_for_keyboard/)

- Install xcape.
- Add the following line to run on every startup: `xcape -e 'Super_L=Alt_L|F3'`
- Map `Alt+F3` to the shortcut you want to run with `super`

# Desktop

- Remove panel 2, bring panel 1 down.
- Add Whisker Menu, remove Applications Menu.

# Create Default Folders

These folders don't exist by default, the commands create them as well as pin as bookmark

- `mkdir -p ~/Pictures/screenshots ~/Documents ~/Music ~/Videos`
- `mkdir -p .config/gtk-3.0/ && >.config/gtk-3.0/bookmarks`
- `printf '%s\n' "file:///home/$USER/Documents" "file:///home/$USER/Pictures" "file:///home/$USER/Videos" "file:///home/$USER/Music" > .config/gtk-3.0/bookmarks`

# Others

- Keyboard setting, repeat delay: 300, repeat speed: 30
- Add to `.bashrc` file: `export EDITOR=nvim`
- Setup AUR, install Espanso through AUR.
