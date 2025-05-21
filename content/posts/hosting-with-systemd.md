+++ 
date = 2024-12-19T03:30:39+08:00
title = "Hosting with Systemd"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

Use Systemd to maintain running processes, simply place a `.service` file into `/etc/systemd/system` and enable it:

# Creating a Unit file:

`sudoedit /etc/systemd/system/myservice.service`

Unit file example:

```
[Unit]
Description=Hello world
After=network.target

[Service]
User=username
Environment=REDIS_HOST=localhost
WorkingDirectory=/home/user/Development/demo-api-redis
ExecStart=/usr/bin/node index.js # full absolute path required if running a script

[Install]
WantedBy=multi-user.target
```

Example with Python app (Flask app with Gunicorn and virtual environment):

```
[Unit]
Description=desc
After=network.target

[Service]
User=username
Environment="PATH=/home/path-to-repo/.venv/bin"
WorkingDirectory=/home/path-to-repo/
ExecStart=/home/path-to-repo/.venv/bin/gunicorn --workers 3 --bind 0.0.0.0:8080 app:app
ExecReload=/bin/kill -s HUP $MAINPID
KillMode=mixed
TimeoutStopSec=5
PrivateTmp=true

[Install]
WantedBy=multi-user.target
```

Run the process:

```
systemctl daemon-reload
systemctl enable demo-api-redis@1
systemctl start demo-api-redis@1
systemctl status demo-api-redis@1
```

## Dependencies in Systemd

`Wants=` directive to the `[Unit]` section

```
...
After=network.target
Wants=redis.service
```

After editing, restart service: `systemctl restart demo-api-redis@1`

# Process management

Under `[Service]` in the unit file:

```
Restart=always
RestartSec=500ms
StartLimitInterval=0
```

tells systemd to always restart the service after a 500ms delay

view the logs, -u for unit file.
`journalctl -u demo-api-redis@1`

add `-f` to follow the latest log:
`$ journalctl -u demo-api-redis@1 -f`

log filter (log, warn, error):
`$ journalctl -u demo-api-redis@1 -p err`

cat the service file:
`systemctl cat demo-api-redis@1`

# Running Multiple Instance

If you name your unit file:
`my-node-app@.service`

and assuming you want 3 instances running, you can do:

`systemctl start my-node-app@{1,2,3}.service`

Address each one process with the number given. For e.g. to get the logs for 1:
`journalctl -u my-node-app@1.service`

You can actually treat a single unit file as a template ([docs over here](https://www.freedesktop.org/software/systemd/man/systemd.unit.html)).

# Ref

https://www.cloudbees.com/blog/running-node-js-linux-systemd#creating-unit-files
