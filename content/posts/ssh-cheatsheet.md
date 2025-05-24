+++ 
date = 2025-05-24T22:49:50+01:00
title = "SSH Cheatsheet"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

# SSH Config

Config file path: `~/.ssh/config`
Format example:

```
host servername
    hostname 123.456.100.200
    user username
    port 22
```

Using proxyjump (ensures the server targetServer is accessed through proxyServer, usage of ip address instead of DNS is faster):

```
host proxyServer # also called bastion/jumphost
    user username
    hostname 143.239.75.153

host targetServer
    user username
    hostname 143.239.82.203 # IP of "targetServer" as seen from "proxyServer" server
    proxyjump proxyServer
```

## SSH Multiplexing

```
Host *
  IdentitiesOnly yes
  controlpath /tmp/ssh-%r@%h:%p
  ControlMaster auto
  ControlPersist yes
```

ref: https://www.cyberciti.biz/faq/linux-unix-reuse-openssh-connection/

# Copy SSH key to server

Generating with ssh-keygen examples:
`ssh-keygen -t rsa`
`ssh-keygen -t ed25519 -f ~/.ssh/your-key-filename -C "your-key-comment"`

Copy to server:
`ssh-copy-id user@hostname.example.com`

[ssh-with-github](/posts/ssh-with-github/)

# SSH Tunnelling

## Local Forwarding (Local Tunnel)

3 machines/host is required:

- Local
- Target
- Proxy/Jumphost/Proxy (publicly accessible)

`ssh -L 9000:imgur.com:80 user@proxy-host-address.com

- Listens to port 9000, just 9000 will do, assumed to be localhost.
- target is to go to imgur.com at port 80
- go through a proxy server with the address `proxy-host-address.com`

Another example:

`ssh -L 22001:localhost:22000`

- Listens to our localhost at port 22001
- maps to the localhost **of the target server** at port 22000. The `localhost` here refers to the server's localhost.

## Remote Forwarding (Reverse Tunnel)

On the server: `sudoedit /etc/ssh/sshd_config`

Change the following to yes:

```
AllowTcpForwarding yes
GatewayPorts yes
X11Forwarding yes
```

`-nNT` flags will cause SSH to not allocate a tty/shell and only do the port forwarding, or just `-N` will do?

`ssh -N -R 143.239.81.132:9000:localhost:22 server`

`ssh -N -R localhost:9000:localhost:22 server`

On the server PC: `ssh -p9000 user@localhost`

Check the listening port on server side:
https://superuser.com/questions/1847101/how-to-find-the-ssh-connection-behind-a-reverse-tunnel-from-the-server-side

Persistense with autoSSH:
https://tecadmin.net/keep-the-ssh-tunnels-alive-with-autossh/
https://handyman.dulare.com/ssh-tunneling-with-autossh/
