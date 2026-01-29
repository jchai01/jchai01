+++ 
date = 2024-02-10T02:04:09Z
title = "Xdotool script examples"
description = ""
slug = ""
authors = []
tags = ["xdotool", "automation", "linux", "automation"]
categories = ["guide"]
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

# Moving the mouse
xdotool mousemove 100 100

# click mouse
xdotool click 1

# click and drag
xdotool mousemove 800 600 # initial position
xdotool mousedown 1
xdotool mousemove 860 700 # after position
xdotool mouseup 1

# scrolling
xdotool click 4 # scroll up
xdotool click 5 # scroll down
xdotool key Page_Down # or just use page up/down
```

## Getting mouse location

`xdotool getmouselocation`

updates every 2 second:
`watch -n0.1 xdotool getmouselocation`

## Ref

https://www.youtube.com/watch?v=feLbkm5aV_0
https://github.com/oidz1234/Examples/blob/master/xdotool_cookie_clicker.sh