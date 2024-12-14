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

`sudo pacman -S --needed base-devel git network-manager-applet thunar-archive-plugin wget bluez bluez-utils arc-icon-theme arc-gtk-theme unzip fuse flameshot redshift copyq tmux neovim libreoffice mpv xcape net-tools obsidian syncthing alacritty xclip`

- network-manager-applet - in order to see the network icon in XFCE.
- thunar-archive-plugin - right click extract feature.

# Keyboard shortcuts

- `super+w`: firefox
- `super+return`: terminal
- `super+i`: `xfce4-settings-manager`
- `print`: `flameshot gui`
- `shift+print`: `flameshot full --clipboard --path /home/user/Pictures/screenshots`
- `super+b`: `pkill -USR1 '^redshift$'`. [Redshift setup reference](/posts/redshift/)
- `super+s`: `sh -c 'firefox "https://www.google.com/search?q=$(xclip -o)"'`. [Google Search hotkey setup reference](/posts/google-search-highlighted-text/)
- `Alt+F3`: `xfce4-popup-whiskermenu`. Maps to `super` eventually, see [super key workaround](#super-key-workaround "jumps to super key workaround")

### Under Window Manager settings

- `super + left/right/up/down` to tile windows.

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

# Nerdfont Installation

```
sudo wget -P /usr/share/fonts https://github.com/ryanoasis/nerd-fonts/releases/download/v3.2.1/Hack.zip && sudo unzip -d /usr/share/fonts/Hack /usr/share/fonts/Hack.zip && sudo rm /usr/share/fonts/Hack.zip
```

# Others

- Add to `.bashrc` file: `export EDITOR=nvim`
- alacritty as default terminal
- Setup AUR: https://itsfoss.com/aur-arch-linux/
- install Espanso through AUR, run on startup: `espanso service register`
- nvim config: git clone https://github.com/jchai01/astrovim-config-v4 ~/.config/nvim
- dotfile setup: https://github.com/jchai01/dotfiles
