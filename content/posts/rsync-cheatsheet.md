+++ 
date = 2025-05-24T22:32:29+01:00
title = "Rsync Cheatsheet"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

## Usage

`rsync [options] [source] [dest]`

`--delete`: delete anything in the target directory that isn't in the source directory (avoid duplicates)
`--dry-run`: run this before the actual command
`-Pravh`: Progress, Recursive, Archive, Verbose, Human Readable
`-z`: apply compression before sending (use for poor internet connection)

## Local PC to server:

`rsync -Pravh file user@server-ip:/home/user/folder`
`rsync -Pravh file user@server-ip:` (Using just a colon would transfer to the home directory of the server):

`servername` is a server in ssh config (`~/.ssh/config`): `rsync -Pravh file servername`

## Server to Local PC (using local PC):

`rsync -Pravh user@server-ip:/home/user/folder localFolder`

## Notes

Remove trailing `/` when transferring folders, so that destination creates a folder instead of throwing every file there:

```bash
ls folderToTransfer
file1
file2
rsync -Pravh folderToTransfer servername:
```

## Troubleshoot

`error in rsync protocol data stream (code 12) at io.c(231) [sender=3.2.7]`:
Ensure rsync is installed in both system, use scp as fallback as it is usually installed by default.
