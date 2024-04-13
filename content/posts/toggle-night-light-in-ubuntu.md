+++ 
date = 2023-12-26T22:58:22Z
title = "Toggle night light in Ubuntu"
description = ""
slug = ""
authors = []
tags = ["ubuntu", "linux"]
categories = ["linux"]
externalLink = ""
series = []
+++

## Set night light to always on

1. Install dconf-editor:
```
sudo apt install dconf-editor
```
2. Open dconf-editor and navigate to the key/org/gnome/settings-daemon/plugins/color/
3. Set night-light-schedule-automatic to false
4. Set night-light-schedule-from to 0, and night-light-schedule-to to 24 (or any value higher than this)


ref: [link](https://askubuntu.com/questions/1087449/force-gnome-night-light-to-stay-on-and-never-turn-off)


## Add custom shortcut to toggle night light 

Use the following script:
```bash
bash -c "if [[ $(gsettings get org.gnome.settings-daemon.plugins.color night-light-enabled) == "true" ]]; then gsettings set org.gnome.settings-daemon.plugins.color night-light-enabled false; else gsettings set org.gnome.settings-daemon.plugins.color night-light-enabled true; fi"
```

Bind it to a shortcut, mine is `super + b`

ref: [link](https://www.reddit.com/r/gnome/comments/ig7wsk/a_keyboard_shortcut_to_toggle_nightlight_in_gnome/)
