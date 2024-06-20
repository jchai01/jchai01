+++ 
date = 2024-06-19T23:48:19+01:00
title = "Vimgrep Cheatsheet"
description = ""
slug = ""
authors = []
tags = ["vim"]
categories = ["vim"]
externalLink = ""
series = []
+++

# Usage

- `:vim /pattern/g **/*.java` adds matches to quickfix list.
- `:vim /pattern/g src/**` means everything in src folder.
- vimgrep is shortened to vim.
- `**/*` means everything.

# Quickfix list

- `:copen` opens quickfix list, can be shortened to `:cope`
- `:cnext` and `:cprev`, can be shortened to `:cn` and `:cp`
- `ctrl-ww` moves window
- `:cc <number>`

# Search and replace project-wide example:

- `cdo: s/textToFind/replaceText | update`
- update saves the buffer, instead of typing :w for all the buffers.

# Notes:

- unimpaired-vim plugin to use shortcuts like `[q` to navigate quickfix list.
- In C, make command already automatically errors into quickfix list.
