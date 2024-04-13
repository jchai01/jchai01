+++ 
date = 2024-01-03T02:47:17Z
title = "FFMPEG cheatsheet"
description = ""
slug = ""
authors = []
tags = ["ffmpeg", "cheatsheet"]
categories = []
externalLink = ""
series = []
+++

### Changing Aspect Ratio

Resizing a video from 4:3 to 16:9 (HD, 1280 x 720) for max screen size, with no cropping and addition of black padding
```bash
ffmpeg -i input.mp4 -vf "scale=(iw*sar)*min(1280/(iw*sar)\,720/ih):ih*min(1280/(iw*sar)\,720/ih),pad=1280:720:(ow-iw)/2:(oh-ih)/2:black" output.mp4
```

Explanation:
*scale = FFMPEG video filter to resize a video
* (iw*sar)*min(1280/(iw*sar)\,720/ih) = output width of the resized video = Resize width of video to AT MOST 1280 (keeping original aspect ratio)
* ih*min(1280/(iw*sar)\,720/ih) = output height of the resized video = Resize width of video to AT MOST 720 (keeping original aspect ratio)

The scale transformation is then followed (chained) by a pad video filter:
* pad = FFMPEG video filter to pad a video with a color
* 1280:720 = Create a black background frame of 1280x720
* (ow-iw)/2:(oh-ih)/2 = Overlay the original film in the middle
* black = the padding color 

Resizing a video from 4:3 to 1:1 (Instagram format) for maximum screen size, with no cropping and addition blue padding
```bash
ffmpeg -i input.mp4 -vf "scale=(iw*sar)*max(1280/(iw*sar)\,720/ih):ih*max(1280/(iw*sar)\,720/ih),pad=1280:1280:(ow-iw)/2:(oh-ih)/2:blue" output02.mp4
```

with:
*scale = FFMPEG video filter to resize a video
* (iw*sar)*max(1280/(iw*sar)\,720/ih) = output width of the resized video = Resize width of video to AT LEAST 1280 (keeping original aspect ratio)
* ih*min(1280/(iw*sar)\,720/ih) = output height of the resized video = Resize width of video to AT LEAST 720 (keeping original aspect ratio)

The scale transformation is then followed (chained) by a pad video filter:
* pad = FFMPEG video filter to pad a video with a color (here color = blue)
* 1280:1280 = Create a black background frame of 1280x1280
* (ow-iw)/2:(oh-ih)/2 = Overlay the original film in the middle
* blue = the padding color 

Credits to The FFMPEG Guy: https://www.youtube.com/watch?v=XKUFShFeqXc

