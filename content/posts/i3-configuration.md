+++ 
date = 2023-12-26T22:45:57Z
title = "I3 configuration"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

My attempt on switching to a window manager (I3). I was on a pretty old laptop (GL752V), probably why I faced a handful of issues. Distro used: EndeavourOS.

config file path:

```bash
~/.config/i3/config
```

Changes made:

- Change open file explorer from ctrl+n to ctrl+e
- Make brightness key work. (See fix i3wm brightness)
- Resize feature with mod + ctrl + arrow keys.
- Ensure power button work.
- Make alt+F4 work as well, other than $mod + q.
- Default dark theme.
- Remove binding of file explorer for workspace 3 (easier to drag and drop files from file explorer to browser.)
- Include xcfe4-screenshooter.
- Change path for default screenshot save location.
- Keybinding to Google search highlighted word. (Mod+s)

Resize:

```bash
bindsym $mod+Ctrl+Right resize shrink width 1 px or 1 ppt
bindsym $mod+Ctrl+Up resize grow height 1 px or 1 ppt
bindsym $mod+Ctrl+Down resize shrink height 1 px or 1 ppt
bindsym $mod+Ctrl+Left resize grow width 1 px or 1 ppt
```

Power Button:

```bash
bindsym XF86PowerOff exec ~/.config/i3/scripts/powermenu
bindsym XF86PowerDown exec ~/.config/i3/scripts/powermenu
```

Alt F4:

```bash
bindsym Mod1+F4 kill
```

Dark theme (SET IN ~/.config/gtk-3.0/settings.ini):

```bash
gtk-application-prefer-dark-theme=1
```

Remove binding of file explorer to workspace 3, comment out:

```bash
# for_window [class=Thunar] focus
```

xcfe4-screenshooter:

```bash
xcfe4-screenshooter -r
```

Copy to clipboard feature after screenshot, install package, then un-comment line:

```bash
sudo pacman -S xfce4-clipman-plugin
```

```bash
exec --no-startup-id xfce4-clipman
```

Change path of screenshot file:

```bash
bindsym Print exec scrot ~/Pictures/%Y-%m-%d-%T-screenshot.png && notify-send "Screenshot saved to ~/Pictures/$(date +"%Y-%m-%d-%T")-screenshot.png"
```

### Fix I3WM Brightness

Download brightnessctl

```bash
sudo pacman -S brightnessctl
```

Add the following line to your config:

```bash
echo 200 > /sys/class/backlight/intel_backlight/brightness
```

```bash
RUN+="/bin/chgrp video /sys/class/backlight/intel_backlight/brightness"
RUN+="/bin/chmod 0664 /sys/class/backlight/intel_backlight/brightness"
```

```bash
/etc/udev/rules.d/backlight.rules
```

```bash
sudo usermod -a -G video chai
```

```bash
sudo -e /etc/udev/rules.d/backlight.rules
```
