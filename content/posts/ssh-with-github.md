+++ 
date = 2024-05-14T23:09:51+01:00
title = "Setup SSH in Github"
description = ""
slug = ""
authors = []
tags = ["github", "linux"]
categories = []
externalLink = ""
series = []
+++

# Create SSH key

`ssh-keygen -o -t rsa -C "any comment"`

- The -o flag forces the tool to generate SSH keys with the OpenSSH format.
- The -t flag specifies the type of SSH keys to create.
- The -C flag allows for comments that get added as metadata at the end of the public key.
- Key generated to `~/.ssh` folder

# View SSH key

`cat ~/.ssh/id_rsa.pub`

# Copy public key to Github

Copy output into `Github > Settings > SSH and GPG keys > New SSH Key`
