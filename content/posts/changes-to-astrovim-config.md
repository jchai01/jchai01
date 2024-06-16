+++ 
date = 2024-01-03T17:34:20Z
title = "AstroNvim config changes"
description = ""
slug = ""
authors = []
tags = ['neovim', 'config']
categories = ['neovim']
externalLink = ""
series = []
+++

Tracking some of the changes I made to the stock AstroNvim. My config: https://github.com/jchai01/astrovim-config-v4.git

# Changes

## Show hidden files in Neo-Tree by default

Under `~/.config/nvim/lua/plugins/neotree.lua`:

```lua
return {
  "nvim-neo-tree/neo-tree.nvim",
  ...
  },
  opts = {
    filesystem = {
      filtered_items = {
	      visible = true,
	      show_hidden_count = true,
	      hide_dotfiles = false,
	      hide_gitignored = true,
	      hide_by_name = {
	        -- '.git',
	        -- '.DS_Store',
	        -- 'thumbs.db',
	      },
	      never_show = {},
      },
    }
  }
}
```

Note: `shift + h` toggles hidden file.

## Add whichwrap

Under `~/.config/nvim/lua/plugins/astrocore.lua`:

`wrap = false, -- sets vim.opt.wrap`

Other ways to do it:

`vim.cmd "set whichwrap+=<,>,[,],h,l"`

## Highlight all text with Leader +a

`["<Leader>a"] = { "<esc>gg0VG", desc = "Select all text" },`

# Plugins

## Debugprint

Automatically adds debug/print statements. [repo](https://github.com/andrewferrier/debugprint.nvim "Link to Debugprint repo")

- `g?v` print statement variable at cursor position, after current line.
- `g?V` print statement variable at cursor position, before current line.
- `g?p` print statement after current line.
- `g?P` print statement before current line.

## surround.nvim

Create a new file named `surorund.nvim` under `~/.config/nvim/lua/plugins`

```lua
return {
  {
    "kylechui/nvim-surround",
    tag = "*", -- Use for stability; omit to use `main` branch for the latest features
    config = function()
    require("nvim-surround").setup({
      -- Configuration here, or leave empty to use defaults
    })
    end,
  },
}
```

- In normal mode: `ysiw` + symbol, for example `)`. (think of `ysiw` as "You Surround In Word")
- In visual mode: after highlighting the word, `shift + s` followed by symbol.

Note: Use the `)` symbol instead of the `(` to ensure no spaces around the surround. My current config [corrects this behaviour](/posts/nvim-surround/)

## vim-signatures

View vim marks.

Create a new file named `vim-signatures.lua` under `~/.config/nvim/lua/plugins`

```lua
return {
    "kshenoy/vim-signature",
    opts = {},
    dependencies = {},
    config = function ()
    end,
}
```

LSP auto formatting messes with vim marks and makes them disappear, haven't found a fix.

# Others

- Ensure latest NodeJS is installed otherwise Javascript LSP won’t work. If you are not on a bleeding edge/rolling release distro, do not install NodeJS with your package manager as it will install older versions.
- `Leader + uw` toggles word wrap. Default behaviour can be defined in `astrocore.lua` too.
