+++ 
date = 2024-02-10T02:04:09Z
title = "Xdotool script examples"
description = ""
slug = ""
authors = []
tags = ["xdotool", "automation", "linux", "automation"]
categories = ["linux", "automation"]
externalLink = ""
series = []
+++

Xdotool is an automation tool in Linux, something like AutoHotKey (AHK) for Windows. Below show some examples of it's usage in a shell script.

```bash
# Type ABC
xdotool key A
xdotool key B
xdotool key C

# Tab 3 times
xdotool key Tab
xdotool key Tab
xdotool key Tab

# Type 20
xdotool key 2
xdotool key 0

xdotool key Down
xdotool key Left
xdotool key Right
xdotool key Return

# Use sleep to wait
sleep 0.5

# Multiple keys
xdotool key ctrl+c
xdotool key Alt+Tab
xdotool key ctrl+f
xdotool key ctrl+v
xdotool key enter
xdotool key super+e

# Loops
for n in {1..1}; 
do
    xdotool key ctrl+c
    xdotool key Alt+Tab

	# Inner loop
    for n in {1..8}; 
    do
        xdotool key Shift_L+Right
    done
done
```

