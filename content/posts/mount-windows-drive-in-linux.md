---
title: "Automount Windows drive in Linux"
date: 2023-12-24T23:10:09Z
---

Find out where the windows drive is located:
```bash
lsblk
```

Edit fstab file:
```bash
sudo nvim /etc/fstab
```

For example, sdb2:
```bash
# <file system>             <mount point>  <type>  <options>  <dump>  <pass>```
/dev/sdb2                      /media/data       ntfs    defaults 0 0

```

Reboot the system:
```bash
reboot
```

Create a launcher.
