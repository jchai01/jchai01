+++ 
date = 2023-12-26T22:57:27Z
title = "Setup latest NeoVim on ubuntu with AppImage"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

Download NeoVim AppImage from GitHub release page.

Rename nvim.appimage to nvim
```bash
mv nvim.appimage nvim
```

Set the permission:
```bash
chmod +x nvim
```

Install fuse2 library if it is required to run the appimage
```bash
sudo apt install libfuse2
```

Copy from download folder to /usr/local/bin path
/usr/bin is used for apps managed by the distribution's package manager, so it's not recommended to copy there.
```bash
sudo mv nvim /usr/local/bin
```
### Optional
Install AstroVim

Download Hack Font

To keep nvim configurations while using sudo:
```bash
sudo -E -s

```
