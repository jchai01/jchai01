---
title: "Automount Windows NTFS drive in Linux"
date: 2023-12-24T23:10:09Z
---

Find out where the windows drive is located: `lsblk -lf`

Edit fstab file (careful, any mistake and Linux would not be able to boot): `sudoedit /etc/fstab`

For e.g. sdb2:

```bash
# <file system>             <mount point>  <type>  <options>  <dump>  <pass>
/dev/sdb2                      /media/data       ntfs    defaults 0 0
```

Reboot the system: `reboot`

Create a launcher, for e.g:

```bash
#!/usr/bin/env xdg-open

[Desktop Entry]
Version=1.0
Type=Application
Terminal=false
Exec=xdg-open /media/data/Users/username/Videos
Name=Open Windows Videos Path
Comment=comment here
Icon=icon path here
```

## Troubleshooting

### In Arch

The newer kernels now use the in-kernel ntfs3 driver, which often fails. When you are mounting them manually, you are using ntfs-3g as the driver, which is the one that works. By blacklisting ntfs3, you make sure that it’ll always use ntfs-3g diver.

```bash
sudo pacman -S ntfs-3g
echo 'blacklist ntfs3' | sudo tee /etc/modprobe.d/disable-ntfs3.conf
```

ref: https://forum.manjaro.org/t/unable-to-automatically-mount-ntfs-external-harddrive-in-thunar/153481
