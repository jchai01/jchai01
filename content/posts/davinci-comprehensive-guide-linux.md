+++ 
date = 2024-06-27T01:54:45+01:00
title = "Davinci Resolve Linux resources"
description = ""
slug = ""
authors = []
tags = ["linux", "davinci resolve"]
categories = ["linux", "davinci resolve"]
externalLink = ""
series = []
+++

# Table of Contents

- [Installation](#installation)
  - [Debugging](#Debugging)
  - [Alternate Installation Method](#AlternateInstallationMethod)
- [Installing GPU Drivers](#InstallingGPUDrivers)
- [H264/H265/AAC Codec Workaround](#H264/H265/AACCodecWorkaround)
  - [FFMPEG Conversion](#FFMPEGConversion)
  - [Smart Folders with Incron](#SmartFolderswithIncron)
  - [Magic Byte Codes](#MagicByteCodes)

## Installation

In general, go to resolve's official site to download and run their installer. If double clicking on icon does not run the app, run the app in the terminal with `/opt/resolve/bin/resolve` and debug from there.

### Debugging

[This video](https://www.youtube.com/watch?v=Y87MFmcy3lc) shows the installation process for Ubuntu 24.04. It includes a comprehensive guide on hunting down and resolving dependencies issues which is useful and applicatble to any linux executable.

### Alternate Installation Method

- Docker/Podman: https://github.com/fat-tire/resolve
- Distrobox: https://www.youtube.com/watch?v=wmRiZQ9IZfc

## Installing GPU Drivers

## H264/H265/AAC Codec Workaround

### FFMPEG Conversion

### Smart Folders with Incron

### Magic Byte codes

Download the studio version from the official site. On an arch system you can use `yay -S davinci-resolve-studio`.

#### Version 18

In the terminal, run ` sudo perl -pi -e 's/\x00\x85\xc0\x74\x7b\xe8/\x00\x85\xc0\xEB\x7b\xe8/g' /opt/resolve/bin/resolve`

#### Version 19

```
cd /opt/resolve

sudo perl -pi -e 's/\x03\x00\x89\x45\xFC\x83\x7D\xFC\x00\x74\x11\x48\x8B\x45\xC8\x8B/\x03\x00\x89\x45\xFC\x83\x7D\xFC\x00\xEB\x11\x48\x8B\x45\xC8\x8B/g' bin/resolve

sudo perl -pi -e 's/\x74\x11\x48\x8B\x45\xC8\x8B\x55\xFC\x89\x50\x58\xB8\x00\x00\x00/\xEB\x11\x48\x8B\x45\xC8\x8B\x55\xFC\x89\x50\x58\xB8\x00\x00\x00/g' bin/resolve

sudo echo -e "LICENSE blackmagic davinciresolvestudio 009599 permanent uncounted\nhostid=ANY issuer=AHH customer=AHH issued=03-Apr-2024\n akey=3148-9267-1853-4920-8173_ck=00 sig=\"00\"\n" > .license/blackmagic.lic
```

Ref: https://www.reddit.com/r/LinuxCrackSupport/comments/1cnslsp/davinci_resolve_studio_19_beta_2_patch_guide/
