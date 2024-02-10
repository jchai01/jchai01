+++ 
date = 2023-12-24T23:58:39Z
title = "Change Timezone in Linux"
description = "Guide on changing the timezone in Linux"
slug = ""
authors = []
tags = ["Linux"]
categories = ["Linux"]
externalLink = ""
series = []
+++

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
