+++ 
date = 2023-12-24T23:58:39Z
title = "Changing Timezone in Linux"
description = "Guide on changing the timezone in Linux"
slug = ""
authors = []
tags = ["Linux"]
categories = ["Linux"]
externalLink = ""
series = []
+++

# Using tzupdate

https://github.com/cdown/tzupdate

Automatically set timezone:

```bash
sudo tzupdate
```

# Manual

View current timezone:

```bash
timedatectl
```

List timezones:

```bash
timedatectl list-timezones
```

Change timezone example:

```bash
sudo timedatectl set-timezone Europe/Dublin
```

If it's still not accurate, try:

```bash
`timedatectl set-ntp true`
```
