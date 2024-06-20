+++ 
date = 2024-06-20T00:59:18+01:00
title = "Connect to Ethernet Manually in Arch Installation medium"
description = ""
slug = ""
authors = []
tags = ["linux"]
categories = ["linux"]
externalLink = ""
series = []
+++

1. Arch installation medium uses **systemd-networkd**
2. Edit the config file: `vim /etc/systemd/network/20-ethernet.network`
3. Edit the `[Network]` portion in the file, write `Address` in CIDR notation.
4. Remove or comment out DHCP related lines.

Example:

```bash
[Network]
Address=192.168.0.132/24
Gateway=192.168.0.254
DNS=192.168.1.2
```
