+++ 
date = 2024-05-14T21:57:33+01:00
title = "Redshift"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

With Redshift, you can set brightness level lower than the minumum.

- `-O` Temperature level (lower = warmer, higher = cooler)
- `-b` Brightness level (0 - 1)

```bash
redshift -oP -O 3500 -b .5
```

Note that calling xrandr on its own will cancel any redshift effect. The -P option of redshift also resets the screen brightness and color instead of incrementally superimposing adjustments.
