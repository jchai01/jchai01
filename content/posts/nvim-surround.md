+++ 
date = 2024-05-15T01:43:37+01:00
title = "nvim.surround overwrite default white space behaviour"
description = ""
slug = ""
authors = []
tags = []
categories = []
externalLink = ""
series = []
+++

Using `(` in nvim.surround surrounds word with white space like so: `( word )`. `)` have to be used instead. The following changes in the `nvim.surround.lua` file overwrites this behaviour.

```bash
return {
  {
    "kylechui/nvim-surround",
    -- tag = "*", -- Use for stability; omit to use `main` branch for the latest features
    config = function()
      require("nvim-surround").setup {
        surrounds = {
          ["("] = {
            add = function() return { { "(" }, { ")" } } end,
          },
          ["{"] = {
            add = function() return { { "{" }, { "}" } } end,
          },
          ["["] = {
            add = function() return { { "[" }, { "]" } } end,
          },
          ["<"] = {
            add = function() return { { "<" }, { ">" } } end,
          },
        },
      }
    end,
  },
}
```
