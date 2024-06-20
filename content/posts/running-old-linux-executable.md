+++ 
date = 2024-06-20T00:14:11+01:00
title = "Running Old Linux Executables Debugging Notes"
description = ""
slug = ""
authors = []
tags = ["linux"]
categories = ["linux"]
externalLink = ""
series = []
+++

# Unclear Error

- `-l` is like an alias for lib, for example: `/usr/bin/ld: cannot find -lXmu: No such file or directory`.
- Actual missing file : `libXmu.so`
- Solution: `sudo apt-get install libxmu-dev`
- reference: https://unix.stackexchange.com/questions/506866/what-should-i-install-to-correct-ld-cannot-find-lgbm-and-linput-so-that-i-c

# Compiling Libraries

- If library is not available in your package manager, need to source from internet, download and compile.
- After running make, the executable .so file usually goes into the **lib folder** from the path where it is compiled.

# Run Executable with library:

`error while loading shared libraries: libGLEW.so.1.10: cannot open shared object file: No such file or directory`

### Solution

`LD_PRELOAD=/home/user/Downloads/glew-1.10.0/lib/libGLEW.so.1.10 ./program-to-run`

OR

1. copy compiled library to `/usr/local/lib`
2. `sudo cp glew-1.10.0/lib/libGLEW.so.1.10 /usr/local/lib`
3. Run `sudo ldconfig` after

# Search for installed library:

`ldconfig -p | grep libpthread.so.0`
