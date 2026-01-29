+++ 
date = 2024-01-02T19:52:20Z
title = "Installing Blender manually in Linux"
description = ""
slug = ""
authors = []
tags = ["blender"]
categories = ["blender"]
externalLink = ""
series = []
+++

Sometimes the package manager does not give you the lastest version of the software. This guide shows you how to install Blender manually without the use of package manager in order to get the lastest version. I am using Ubuntu in this example.

1. Download the zip file from Blender website. Unzip the file.

2. Copy the extracted folder to somewhere else if you want to. For me I placed them in /opt folder. I have renamed the folder to just "blender":

```bash
sudo mv -r blender /opt
```

Create desktop entry by creating an empty textfile with the .desktop extension:

```bash
touch blender.desktop
```

3. Enter the desktop entry, remember to change the exec path to where you installed Blender to.
   To associate .blend file with Blender. the %F flag is important in the exec statement.
   An example of the desktop entry:

```
[Desktop Entry]
Type=Application
Name=Blender
GenericName=Blender
Path=/opt/blender/
Exec=/opt/blender/blender %F
Terminal=false
Icon=/opt/blender/blender.svg
StartupNotify=true
Name[en_US]=Blender
MimeType=application/x-blender;
```

4. Remember to set the permission to execute the desktop entry:

```bash
sudo chmod +x blender.desktop
```

5. Copy/move desktop entry to usr/share/application, this allows you to search for Blender.

```bash
sudo cp blender.desktop /usr/share/applications
```

6. Create link to usr/local/bin, this allows you to use blender through the terminal.

```bash
sudo ln -s path_to_blender_executable /usr/local/bin
```

## Updating

1. Remove the current Blender installation: `sudo rm -rf /opt/blender`
2. Obtain the blender tar.xz file from the official website.
3. Extract the tar file to the correct path: `sudo tar -xf blender-<version>.tar.xz -C /opt`
4. Rename the folder: `sudo mv /opt/blender-<version> /opt/blender`
5. Remove the tar file `rm blender.tar.xz`
