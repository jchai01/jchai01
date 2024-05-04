+++ 
date = 2024-05-03T18:41:41+01:00
title = "Tmuxifier Guide"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

If you have ever tried to write a shell/batch script to automate a whole dev environment such as running backend servers/opening code editor etc, this guide is for you.

Pre-requisite: Tmux

I have set the alias `alias tm=tmuxifier` in this guide.

### Tmuxifier Path

- To delete/rename sessions, go to this path and manipulate the files. (not sure why there isn't a command for these operations)
- If you have created a session before, you can `cd` into this path and duplicate the files etc, to create your sessions too.

```bash
~/.tmuxifier/layouts/
```

### Create a session

ns = new-session

```bash
tm ns name-of-session
```

### Example session template

In this example, it starts:
- several docker containers based on the yaml file
- a frontend-server
- a backend-server (geoserver) that isn't dockerized
- opens the editor.

```bash
# Set a custom session root path. Default is `$HOME`.
# Must be called before `initialize_session`.
session_root "~/repos/your-project-path/"

# Create session with specified name if it does not already exist. If no
# argument is given, session name will be based on layout file name.
if initialize_session "your-session-name"; then

  # Create a new window inline within session layout definition.
  new_window "docker"
  new_window "frontend-server"
  new_window "geoserver"
  new_window "vim"

  select_window "docker"
  run_cmd "cd ../your-project-path/docker/"
  run_cmd "docker compose -f docker-compose.dev.yaml up -d"

  select_window "frontend-server"
  run_cmd "npm start"

  select_window "geoserver"
  run_cmd "sh /usr/share/geoserver/bin/startup.sh"

  select_window "nvim"
  run_cmd "nvim ."

  # Select the default active window on session creation.
  #select_window 1

fi

# Finalize session creation and switch/attach to it.
finalize_and_go_to_session
```

### Running a session

Make sure you are not using your terminal inside Tmux, then run:

```bash
tm s name-of-session
```

### Editing a session

```bash
tm es name-of-session
```
