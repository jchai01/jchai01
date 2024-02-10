+++ 
date = 2024-01-11T15:27:40Z
title = "Python Cheatsheet"
description = ""
slug = ""
authors = []
tags = ["Python"]
categories = []
externalLink = ""
series = []
+++

### Virtual Environment

In this example, folder for the Virtual Environment is .venv

```bash
python3 -m venv .venv
```

```bash
source .venv/bin/activate
```

```bash
deactivate
```

### Packages

```bash
pip install name-of-package
```

```bash
pip uninstall name-of-package
```

```bash
pip install -r requirements.txt
```

### pyenv
Manage different versions of python.

List all version installed:
```bash
pyenv versions
```

Switch to a particular version example:
```bash
pyenv global 3.8
```

Reset back to default:
```bash
pyenv global system
```

List all version available for install:
```bash
pyenv install -l
```

Install a python version example:
```bash
pyenv install 3.8
```

Install a python version example:
```bash
pyenv install 3.8
```

If installation of python version fail, ensure dependencies are installed:
```bash
sudo apt update
sudo apt install \
    build-essential \
    curl \
    libbz2-dev \
    libffi-dev \
    liblzma-dev \
    libncursesw5-dev \
    libreadline-dev \
    libsqlite3-dev \
    libssl-dev \
    libxml2-dev \
    libxmlsec1-dev \
    llvm \
    make \
    tk-dev \
    wget \
    xz-utils \
    zlib1g-dev
```

