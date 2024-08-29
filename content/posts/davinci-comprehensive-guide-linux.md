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

{{<toc>}}

## Installation

Go to resolve's official site to download and run their installer. If double clicking on icon does not run the app, run the app in the terminal with `/opt/resolve/bin/resolve` and debug from there.

### Debugging

[This video](https://www.youtube.com/watch?v=Y87MFmcy3lc) shows the installation process for Ubuntu 24.04. It includes a comprehensive guide on hunting down and resolving dependencies issues which is useful and applicable to any linux executable.

### Alternate Installation Method

I have not personally tried these methods.

- Docker/Podman: https://github.com/fat-tire/resolve
- Distrobox: https://www.youtube.com/watch?v=wmRiZQ9IZfc

## H264/H265/AAC Codec Workaround

### FFMPEG Conversion

```
for file in *.mp4 ; do ffmpeg -i ${file} -crf 16 -c:v libx264 -c:a aac outfolder/`basename ${file} .mp4`-16.mp4 ; done
```

### Smart Folders with Incron

https://www.reddit.com/r/davinciresolve/comments/15ldzah/solution_to_the_mp4_h264_h265_issue_on_linux/
https://passthroughpo.st/painless-linux-video-production-part-3-organization-and-workflow/

### Transcode specific footage on the fly while editing.

This is a Studio specific problem, as the studio version still does not support AAC codec.

This script I wrote that converts footage on the fly with a hotkey: https://github.com/jchai01/davinci-resolve-aac-workaround-macro

### Magic Byte codes

This is one way to workaround several Linux-specific annoyances. Consider supporting them and paying for their product especially if you are making money from it.

Download link to the davinci-resolve-studio installer can be found here: https://www.blackmagicdesign.com/support/family/davinci-resolve-and-fusion

On an arch system, you can use `yay -S davinci-resolve-studio`.

#### Version 18

In the terminal, run ` sudo perl -pi -e 's/\x00\x85\xc0\x74\x7b\xe8/\x00\x85\xc0\xEB\x7b\xe8/g' /opt/resolve/bin/resolve`

#### Version 19 beta (tested on beta 3 & 4)

```
cd /opt/resolve

sudo perl -pi -e 's/\x03\x00\x89\x45\xFC\x83\x7D\xFC\x00\x74\x11\x48\x8B\x45\xC8\x8B/\x03\x00\x89\x45\xFC\x83\x7D\xFC\x00\xEB\x11\x48\x8B\x45\xC8\x8B/g' bin/resolve

sudo perl -pi -e 's/\x74\x11\x48\x8B\x45\xC8\x8B\x55\xFC\x89\x50\x58\xB8\x00\x00\x00/\xEB\x11\x48\x8B\x45\xC8\x8B\x55\xFC\x89\x50\x58\xB8\x00\x00\x00/g' bin/resolve

sudo echo -e "LICENSE blackmagic davinciresolvestudio 009599 permanent uncounted\nhostid=ANY issuer=AHH customer=AHH issued=03-Apr-2024\n akey=3148-9267-1853-4920-8173_ck=00 sig=\"00\"\n" > .license/blackmagic.lic
```

#### Version 19

`sudo /usr/bin/perl -pi -e 's/\x74\x11\xe8\x21\x23\x00\x00/\xeb\x11\xe8\x21\x23\x00\x00/g' /opt/resolve/bin/resolve`

Reference:
https://www.reddit.com/r/LinuxCrackSupport/comments/1f17xw6/davinci_resolve_studio_19_crack_for_linux/
https://www.reddit.com/r/LinuxCrackSupport/comments/1cnslsp/davinci_resolve_studio_19_beta_2_patch_guide/
https://www.reddit.com/r/davinciresolve/comments/l73wyu/found_a_link_for_just_davinci_downloads/

## I can't move or maximize my Davinci Resolve window around

- Hold down the `super` key and drag the window around with your mouse.
- `alt+F10` is usually the hotkey to maximize the window of any software.

## More Resources

https://wiki.archlinux.org/title/DaVinci_Resolve
https://alecaddd.com/davinci-resolve-ffmpeg-cheatsheet-for-linux/
