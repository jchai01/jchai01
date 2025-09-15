+++ 
date = 2025-09-13T18:34:07+01:00
title = "Google Translate Hotkey Example"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

Example which translate chinese words, just highlight the word and hit `super + z` (in my case)

```bash
wmctrl -a Firefox && sh -c 'firefox "https://translate.google.com/?sl=zh-CN&tl=en&text=$(xclip -o)"'
```
