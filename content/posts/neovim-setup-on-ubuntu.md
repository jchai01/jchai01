+++ 
date = 2023-12-26T22:57:27Z
title = "Setup Latest NeoVim Guide"
description = ""
slug = ""
authors = []
tags = ["linux", "neovim"]
categories = ["linux"]
externalLink = ""
series = []
+++

# Executable

- Download the NeoVim tar file. Extract and copy folder into /opt/

```
sudo mv nvim-folder /opt
```

- Create symbolic link/symlink to `/usr/local/bin`

```
sudo ln -s /opt/nvim-some-version/nvim /usr/local/bin
```

# AppImages

- Download NeoVim AppImage from GitHub release page.

- Rename nvim.appimage to nvim

```bash
mv nvim.appimage nvim
```

- Set the permission:

```bash
chmod +x nvim
```

- Install fuse2 library if it is required to run the appimage

```bash
sudo apt install libfuse2
```

- Copy from download folder to `/usr/local/bin` path

`/usr/bin` is used for apps managed by the distribution's package manager, so it's not recommended to copy there.

```bash
sudo mv nvim /usr/local/bin
```

# Optional

### Font Installation

Download [nerdfonts](https://www.nerdfonts.com/font-downloads). Just extract the tar file and throw the whole folder into: `/usr/share/fonts`

```bash
sudo mv some-path/foldername /usr/share/fonts
```

### Set NeoVim as the default editor

Add the this line: `export EDITOR="nvim"` to the `.bashrc` file:

### Alias v to nvim

`alias v="nvim"`

### Install AstroNvim

### To keep nvim configurations while using sudo:

`sudo -E -s`
