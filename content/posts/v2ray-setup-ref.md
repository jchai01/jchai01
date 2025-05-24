+++ 
date = 2025-05-24T22:30:56+01:00
title = "V2Ray Self-Hosted Setup Reference"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

Note: it seems like v2Ray have been superseded by xRay + XLTS, might want to look into that next time.

# Server

```
curl -O https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh
sudo bash install-release.sh
sudo systemctl restart v2ray
sudo systemctl enable v2ray
```

config:
`/usr/local/etc/v2ray/config.json`

On a UNIX system, you can generate random UUID with:
`cat /proc/sys/kernel/random/uuid
`
Change:

- UUID (use the same for client too, it's used to encrypt/decrypt traffic)
- path
- port

```
{
  "log": {
    "loglevel": "warning",
    "access": "/var/log/v2ray/access.log",
    "error": "/var/log/v2ray/error.log"
  },
  "inbounds": [
    {
      "port": 9999,
      "listen":"127.0.0.1",
      "protocol": "vmess",
      "settings": {
        "clients": [
          {
            "id": "7b317df0-eab4-431f-be92-fbad2cc7e51e", # CHANGE UUID
            "alterId": 64
          }
        ]
      },
      "streamSettings": {
        "network": "ws",
        "wsSettings": {
        "path": "/ray" # USE CORRECT PATH
        }
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "freedom",
      "settings": {}
    }
  ]
}
```

# Nginx

Setup up domain name + HTTPS with LetsEncrypt/Certbot

Config should look something like:

```
server {
      server_name domain-name www.domain-name;

      index index.html;
      root /usr/share/nginx/html/;

      access_log /var/log/nginx/v2ray.access;
      error_log /var/log/nginx/v2ray.error;

      location /ray/ {
            if ($http_upgrade != "websocket") {
              # Return 404 error when WebSocket upgrading negotiate failed
              return 404;
            }
                  proxy_redirect off;
                  proxy_pass http://127.0.0.1:9999; # match server config port
                  proxy_http_version 1.1;
                  proxy_set_header Upgrade $http_upgrade;
                  proxy_set_header Connection "upgrade";
                  proxy_set_header Host $host;

                  # Show real IP in v2ray access.log
                  proxy_set_header X-Real-IP $remote_addr;
                  proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
            }

        listen 443 ssl;
        ssl_certificate /etc/letsencrypt/live/domain-name/fullchain.pem;
        ssl_certificate_key /etc/letsencrypt/live/domain-name/privkey.pem;
        include /etc/letsencrypt/options-ssl-nginx.conf;
        ssl_dhparam /etc/letsencrypt/ssl-dhparams.pem;
    }

    server {
        if ($host = domain-name) {
            return 301 https://$host$request_uri;
        }

    listen 80;
            server_name domain-name;
        return 404;
    }
```

## Router

forward public port 443 to LAN port 443

# Client

## Linux

Run: `v2ray`
Run with config: `v2ray -c /etc/v2ray/config.json`

in Ubuntu, 4.34 does not work, need to use 4.28.2

```
{
  "inbounds": [
    {
      "port": 9999,
      "listen": "127.0.0.1",
      "protocol": "socks",
      "sniffing": {
        "enabled": true,
        "destOverride": ["http", "tls"]
      },
      "settings": {
        "auth": "noauth",
        "udp": false
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "vmess",
      "settings": {
        "vnext": [
          {
            "address": "domain-name", # without the https:// would work
            "port": 443,
            "users": [
              {
                "id": "7b317df0-eab4-431f-be92-fbad2cc7e51e", # has to match the server's UUID
                "alterId": 0
              }
            ]
          }
        ]
      },
      "streamSettings": {
        "network": "ws",
        "security": "tls",
        "wsSettings": {
          "path": "/ray" # path has to change accordingly in server's config and nginx
        }
      }
    }
  ]
}
```

## Android

Download v2RayNG
Create new config: `Type manually[vMess]`
address: `domain-name`
port: `443`
id: UUID that has to match the server, for e.g. `7b317df0-eab4-431f-be92-fbad2cc7e51e`
Security: `chacha20-poly1305`

Transport:
Network: `ws` (web socket)
ws path: `/ray` (has to match nginx config)
allow insecure: `false`

Ref:
https://www.linuxbabe.com/ubuntu/set-up-v2ray-proxy-server
https://gist.github.com/Hansimov/05ae4e81bc8349131e939ed4753304db

## Troubleshoot

Ensure server time is synced: https://askubuntu.com/questions/1314479/ntp-not-supported
