+++ 
date = 2024-10-21T22:57:46+01:00
title = "Arch Install reference"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

This guide provides instructions for steps that isn't explained well/in detail by Arch Wiki.

## Patitioning Disk with Fdisk

### Selecting the disk

- Use `sudo fdisk -l` or `lsblk` to list the disk in your computer (`lsblk` gives less details).
- Select the appropriate disk to operate on with `sudo fdisk /dev/sda` (be sure to double check the correct disk is selected as it will be wiped).

### Create partitions

- boot, root and swap (optional) partition.
- For each partition, we need to set a **partition type** and **file system format** (Partition type will be set first with fdisk).
- Partition type: Linux Filesystem, EFI System, Linux Swap
- File system type: FAT32, NTFS, VFAT etc.

| Partition      | Partition Type   | File System Format    |
| -------------- | ---------------- | --------------------- |
| boot           | EFI System       | FAT32                 |
| swap(optional) | Linux Swap       | No file system format |
| root           | Linux Filesystem | ext4                  |

`g` to create a GPT label (for UEFI system), `o` for DOS/MBR partition (legacy BIOS)
both of these clears the drive of any previous partitions and starts from clean slate.

#### Boot partition

- `n` to create a new partition. `+1G` to give it 1GB of space.
- After creating, `t` to set the type, `ef` to set the type EFI partition.
- `+512M` for e.g. to allocate 512MB of space.
- Best to allocate 1GB of space for boot partition as recommended by Arch wiki (encountered an issue trying to install NVIDIA proprietary driver, turns out the boot partition ran out of space).

#### Swap partition (Optional)

- `n`. `+4G`. (example for 4GB)
- `t`, Change the value to 82 (Linux Swap).

#### Root partition

- `n`. Press enter multiple times to use the default value (the rest of the disk space).

Once everything is done, `w` to write, this change is permanent.

### Formatting and Setting Filesystem Type

#### FAT32 for boot partition:

`mkfs.fat -F32 /dev/sda1`

#### EXT4 for root partition:

`mkfs.ext4 /dev/root_partition`

#### Enable Swap partition

Swap: for example sda2 is for swap.
`mkswap /dev/sda2`
`swapon /dev/sda2`

Root partition mounted on /mnt: `mount /dev/sda3 /mnt`

`pacstrap -K /mnt base linux linux-firmware sudo nano`
`-K` is to create an empty keyring.

Generate filesystem table: `genfstab -U /mnt >> /mnt/etc/fstab` then `arch-chroot /mnt` to go into the installed system.

## Creating User

- `useradd -m -G wheel -s /bin/bash username`
- adding `-s /bin/bash` resolved an issue where the password entered is always incorrect when trying to login.

## Installing XFCE4 Desktop Environment

xfce4 installation: `sudo pacman -S xfce4 xfce4-goodies lightdm light-gtkgreeter`

`systemctl enable lightdm`
`systemctl enable NetworkManager`

## Others

`ctrl-alt-f2` to enter terminal if stuck at booting.

## Ref

- https://wiki.archlinux.org/title/Installation_guide
