+++ 
date = 2024-10-21T22:57:46+01:00
title = "Arch Install Reference/Guide"
description = ""
slug = ""
authors = []
tags = ["linux"]
categories = ["guide"]
externalLink = ""
series = []
+++

This guide provides in-detail instructions for steps in Arch installation, a reference for myself.

Pre-requisites:
- disable CSM in bios to prevent errors on GRUB installation.

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

- `n` to create a new partition.
- Hit enter on the first sector, for the last sector: `+1G` to give it 1GB of space.
- After creating, `t` to set the type, `ef` to set the type EFI partition.
- `+512M` for e.g. to allocate 512MB of space.
- Best to allocate 1GB of space for boot partition as recommended by Arch wiki (encountered an issue trying to install NVIDIA proprietary driver, turns out the boot partition ran out of space).

#### Swap partition (Optional)

- `n`. `+4G`. (example for 4GB)
- `t`, Change the value to 82 (Double check, value for Linux swap might change).

#### Root partition

- `n`. Press enter multiple times to use the default value (the rest of the disk space).

Once everything is done, `w` to permanently write.

### Formatting and Setting Filesystem Type

use `lsblk` to ensure you are formatting the correct partition (sda1/sda2 etc...)

#### FAT32 for boot partition:

`mkfs.fat -F32 /dev/sda1`

#### EXT4 for root partition:

`mkfs.ext4 /dev/root_partition`

#### Enable Swap partition

Swap: for example sda2 is for swap.
`mkswap /dev/sda2`
`swapon /dev/sda2`

### Mounting & Installing

- Mount root partition on `/mnt`: `mount /dev/sda3 /mnt`
- Install Linux: `pacstrap -K /mnt base linux linux-firmware sudo vi`
  `-K` is to create an empty keyring.
- Generate filesystem table: `genfstab -U /mnt >> /mnt/etc/fstab`
- `arch-chroot /mnt` to go into the installed system.

## Grub Installation

- `pacman -S grub efibootmgr`
- `mkdir /boot/efi`
- `mount /dev/efi-partition /boot/efi`
- `grub-install --target=x86_64-efi --bootloader-id=grub_uefi --recheck`
- `grub-mkconfig -o /boot/grub/grub.cfg`

ref: https://gist.github.com/chriscandy/16899e0d701a05654cb4f79ef2d2d062

## Creating User

- `passwd` to set a root password, the default root password is an invalid one.
- `useradd -m -G wheel -s /bin/bash username`
- edit the visudo file to allow users in wheel group to use sudo: `sudo visudo` (uncomment the appropriate lines)
- adding `-s /bin/bash` resolved an issue where the password entered is always incorrect when trying to login.
- `passwd username` to set a password.

## Install GRUB Bootloader

- Disable CSM (compatibility support module) support in BIOS

## Installing XFCE4 Desktop Environment

xfce4 installation: `sudo pacman -S xfce4 xfce4-goodies networkmanager lightdm lightdm-gtk-greeter`
Enable services: `systemctl enable lightdm` & `systemctl enable NetworkManager`

## GPU Driver installation

- for certain nvidia card, running: `sudo pacman -S nvidia-open nvidia-utils nvidia-settings` and rebooting the pc should work.
- otherwise, refer to the full guide: https://github.com/korvahannu/arch-nvidia-drivers-installation-guide
- check if nvidia driver is installed with `nvidia-smi`.

## Others

- `ctrl-alt-f2` to enter terminal if stuck at booting.
- If accidentally logout from installation medium, default password is `root`.

## Post Installation

- [My Arch XFCE changes](/posts/arch-xfce-changes)

## Ref

- https://wiki.archlinux.org/title/Installation_guide
