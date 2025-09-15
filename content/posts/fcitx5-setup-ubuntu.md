+++ 
date = 2025-09-13T18:38:53+01:00
title = "FCITX5 Setup Ubuntu for Chinese Keyboard"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

Switching to fcitx5 as I was unable to change the iBus input font size (way too small).

Install:

```bash
sudo apt install fcitx5 fcitx5-chinese-addons fcitx5-diagnose fonts-noto-cjk fonts-noto-cjk-extra `im-config`
```

Update font cache:

```bash
sudo fc-cache -f -v
```

Add environment variahbles:

Recommended (`sudoedit /etc/environment`):

```
XMODIFIERS=@im=fcitx5
GTK_IM_MODULE=fcitx5
QT_IM_MODULE=fcitx5
```

Add to .bashrc file and reload (not recommended):

```
export XMODIFIERS=@im=fcitx5
export GTK_IM_MODULE=fcitx5
export QT_IM_MODULE=fcitx5
```

Run and select fcitx5 as the default input method:

```
`im-config -c`
```

Run:

```
`fcitx5-configtool`
```

Add `fcitx5` to startup application in Ubuntu

Setting `super + space` to switch input type:
disable Ubuntu's `super + space` shortcut `settings > keyboard shortcuts`, so it doesn't clash. Set it in fcitx's setting to super+space instead.

Issues:
In some browser page, `super + space + space` is needed to switch input type, not sure why.

## Ref

https://medium.com/@brightoning/cozy-ubuntu-24-04-install-fcitx5-for-chinese-input-f4278b14cf6f
