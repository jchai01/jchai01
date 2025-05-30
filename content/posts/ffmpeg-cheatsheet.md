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

## Changing Aspect Ratio

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

The FFMPEG Guy: https://www.youtube.com/watch?v=XKUFShFeqXc

## Convert to WhatsApp compatible format

`fmpeg -i broken.mp4 -c:v libx264 -profile:v baseline -level 3.0 -pix_fmt yuv420p working.mp4`

- `-profile:v baseline -level 3.0` makes the file more compatible with most older players, including WhatsApp. Although, it disables some advanced features.
- `-pix_fmt yuv420p` is necessary to compile to baseline (YUV planar color space with 4:2:0 chroma subsampling).
- https://stackoverflow.com/questions/39887869/ffmpeg-whatsapp-video-format-not-supported

## Convert to Instagram compatible format

- Seems like IG post for videos require a yuv420p format too to avoid the "Will Auto-Post When Possible" error.
- `ffmpeg -i file.mp4 -vf format=yuv420p out.mp4`

## Trimming videos:

`ffmpeg -ss 00:00:03 -i file.mp4 -c copy output.mp4`
- trims from 3 sec to the end
- `-c copy` trims without re-encoding video and audio
