# mini.omnipick

A Neovim plugin that extends `mini.pick` with an "omni" picker, combining files, directories, recent files, and git-changed files into a unified interface.


## Demo


https://github.com/user-attachments/assets/b6855903-6be3-4068-842b-5876ad34071c



## Features

- **Unified Search**: Searches files and directories using `fd` (or custom command).
- **Recent Files**: Integrates with `mini.visits` for recently accessed files within the current working directory.
- **Git Status Highlights**: Highlights modified files with customizable highlight groups.
- **Buffers**: Includes currently open buffers in the results.
- **Additional Items**: Forces inclusion of specified files (e.g., `.env`, `.envrc`) even if ignored by `.gitignore`.
- **Icons**: Optional icon display using `mini.icons`.

## Requirements

- Neovim >= 0.9
- `mini.pick` (required)
- `mini.visits` (optional, for recents)
- `mini.icons` (optional, for icons)
- `fd` or custom command using other tools (for file searching)

## Installation

Using [lazy.nvim](https://github.com/folke/lazy.nvim):

```lua
{
  "nvim-mini/mini.pick",
  version = "*",
  dependencies = {
    { "nvim-mini/mini.visits", version = "*" }, -- optional
    { "pirey/mini.omnipick" }, -- required
  },
  config = function()
    -- required
    require("mini.pick").setup()

    -- optional
    require("mini.visits").setup()

    -- required
    require("mini.omnipick").setup()
  end,
}
```

## Setup

Add to your Neovim config:

```lua
require('mini.omnipick').setup({
  -- Optional: Customize highlight groups for git status
  hl_groups = {
    added = 'OkMsg',
    modified = 'WarningMsg',
  },
  -- Optional: Additional items to always include
  additional_items = { '.env', '.envrc' },
  -- Optional: Show directories in results (ignored if using custom command)
  show_dir = false,
  -- Optional: Custom command for file search (defaults to fd)
  command = { 'find', '.', '-type', 'f' },
  -- Optional: Source name in picker
  source_name = 'Omni',
  -- Optional: Show icons
  show_icons = true,
})
```

## Usage

Call the omni picker:

```lua
:Pick omni
```

Or in Lua:

```lua
require('mini.pick').registry.omni()
```

The picker will display a merged list of:
- Git-changed files (highlighted)
- Open buffers
- Recent files (from `mini.visits`)
- All files/directories (from `fd` or custom command)
- Additional specified items

## Credits

This plugin builds upon the excellent [mini.nvim](https://github.com/echasnovski/mini.nvim) ecosystem by echasnovski.

Inspired by [this Reddit post](https://www.reddit.com/r/neovim/comments/1d9d4uo/my_combined_files_directories_and_recents_picker/).

Shoutout to [fff.nvim](https://github.com/dmtrKovalenko/fff.nvim) for the idea of the ultimate file searching tool.

## License

MIT
