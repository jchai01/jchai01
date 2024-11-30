+++ 
date = 2024-11-05T12:54:39Z
title = "Drawing a Circle in SDL3"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

Surprisingly, the SDL library does not provide a way to draw a circle natively. Circles are usually drawn with the usage of [sdl2-gfx](https://www.ferzkopp.net/Software/SDL2_gfx/Docs/html/index.html) or implementing the [midpoint algorithm](https://discourse.libsdl.org/t/query-how-do-you-draw-a-circle-in-sdl2-sdl2/33379).

At the time of writing (11/05/2024), the sdl2-gfx library isn't updated to be compatible with SDL3 yet. This example ports the filledCircleRGBA() method manually: https://github.com/jchai01/comp4300-with-sdl/tree/main/a1

## Steps

- Search and extract the desired function in the header file [SDL2_gfxPrimitives.h](https://www.ferzkopp.net/Software/SDL2_gfx/Docs/html/_s_d_l2__gfx_primitives_8h_source.html)
- Extract the function along with all the other function it depends on from [SDL2_gfxPrimitives.c](https://www.ferzkopp.net/Software/SDL2_gfx/Docs/html/_s_d_l2__gfx_primitives_8c_source.html)
- Fix any errors by following the [SDL3 migration guide](https://github.com/libsdl-org/SDL/blob/main/docs/README-migration.md)
