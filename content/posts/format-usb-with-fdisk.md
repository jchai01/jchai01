+++ 
date = 2024-06-20T01:11:00+01:00
title = "Format Flashdrive with fdisk"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

1. `lsblk` to check which drive to format. `sudo fdisk -l` can be used too for more details.
2. Unmount drive: `umount /dev/sdb1`
3. Select the drive, without the number (sdc instead of sdc1): `sudo fdisk /dev/sdc`
4. `g` to create new GPT partition
5. `n` to write new partition
6. press enter to use default value, entire drive
7. `w` to to write.
8. `lsblk` again to confirm.
9. Set filesystem type e.g. fat32. Select the partition, this time with the number (sdc1): `sudo mkfs.fat -F 32 -n LABEL /dev/sdc1`
