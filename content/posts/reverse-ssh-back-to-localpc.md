+++ 
date = 2024-11-29T03:46:15Z
title = "How to SSH Back to Local Machine Via Reverse Shell"
description = ""
slug = ""
authors = []
tags = ["linux", "ssh"]
categories = []
externalLink = ""
series = []
+++

## Situation

Your local machine is connected to the internet via a router that do not have control over. You are able to SSH into your work machine in another building/office without issues (connected via ethernet with static IP etc), but what if you want SSH access back to your local machine while in office? This can be achieved with reverse shell.

## Configuration

On the work machine (which acts as the server too): `sudoedit /etc/ssh/sshd_config`

Change the following to yes:

```
AllowTcpForwarding yes
GatewayPorts yes
```

Run the following command on the local machine: `ssh -N -R 9000:localhost:22 user@server-ip`

This command makes the server listen on port 9000 (arbitrary port number) for any connections, any connection made is routed to localhost at port 22 on the local machine.

`-R` signifies a reverse tunnel
`-N` prevents shell from opening to the server, just open the tunnel.

On the work machine/server PC: `ssh -p9000 user@localhost`

## Persistence with AutoSSH

Prerequisites: passwordless login to your server with ssh-keygen.

Ensure the tunnel stays alive with autossh: `autossh -M 0 -o "ServerAliveInterval 30" -o "ServerAliveCountMax 3" -N -R 9000:localhost:22 user@server-ip`

- The -M 0 option tells Autossh to use a built-in monitoring port to detect if the SSH tunnel has disconnected.
- The -o "ServerAliveInterval 30" and -o "ServerAliveCountMax 3" options tell Autossh to send keepalive packets every 30 seconds, and to attempt to reconnect if three consecutive keepalive packets fail.

ref: https://tecadmin.net/keep-the-ssh-tunnels-alive-with-autossh/
