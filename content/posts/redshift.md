+++ 
date = 2024-05-14T21:57:33+01:00
title = "Redshift Guide"
description = ""
slug = ""
authors = []
tags = ["linux"]
categories = ["linux"]
externalLink = ""
series = []
+++

# Toggle + Location Agnostic Setup

Create/edit the file `~/.config/redshift/redshift.conf`, set temp-day and temp-night to the same value. lat and lon can be set randomly as it doesn't matter. Example:

```
[redshift]
temp-day=3500
temp-night=3500
fade=0
location-provider=manual

[manual]
lat=48.864716
lon=2.349014
```

Set startup to run `redshift`. Enable toggle with `pkill -USR1 '^redshift$'`, bind it to a hotkey.

# Manual Usage

With Redshift, you can set brightness level lower than the minumum.

- `-O` Temperature level (lower = warmer, higher = cooler)
- `-b` Brightness level (0 - 1)

`redshift -oP -O 3500 -b .5`

Note that calling xrandr on its own will cancel any redshift effect. The `-P` option of redshift also resets the screen brightness and color instead of incrementally superimposing adjustments.
