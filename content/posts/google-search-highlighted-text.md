+++ 
date = 2023-12-26T22:42:42Z
title = "Google search highlighted text"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

```bash
#!/bin/bash

# Google search the highlighted text (requires: xdg-utils, xsel)
xdg-open "[https://google.com/search?q=$(xsel)](https://google.com/search?q=$(xsel))"
```

Bind it to a shortcut key, mine is super + s.
```bash
/home/user/Desktop/scripts/google-search.sh
```
