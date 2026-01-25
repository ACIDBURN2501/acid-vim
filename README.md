# acid-vim

My personal ultralight Neovim configuration.

This repo is intentionally small: a single `init.lua` using `vim-plug`.

## Features

- Simple plugin management via `vim-plug`
- File explorer via `neo-tree`
- Fuzzy finding + grep via `telescope.nvim`
- LSP tooling via `mason.nvim` + minimal LSP setup
- Statusline via `vim-airline`
- Cursor trail via `smear-cursor.nvim`
- Local/remote LLM editing/completions via `llama.vim`

## Plugins

- `folke/tokyonight.nvim`: colorscheme
- `vim-airline/vim-airline`: statusline
- `vim-airline/vim-airline-themes`: extra airline themes
- `nvim-neo-tree/neo-tree.nvim`: file explorer
  - deps: `nvim-lua/plenary.nvim`, `nvim-tree/nvim-web-devicons`, `MunifTanjim/nui.nvim`
- `nvim-telescope/telescope.nvim`: fuzzy finding + `live_grep`
- `williamboman/mason.nvim`: installer/manager for LSP servers and tooling
- `williamboman/mason-lspconfig.nvim`: mason integration for LSP servers
- `neovim/nvim-lspconfig`: LSP server configs (only used as fallback on older Neovim)
- `sphamba/smear-cursor.nvim`: cursor smear animation
- `ggml-org/llama.vim`: LLM-based FIM + instruct editing

## Requirements

- Neovim (0.11+ recommended)
- `git`
- `curl` (used by `vim-plug` bootstrap + `llama.vim`)
- `rg` (ripgrep) for Telescope `live_grep`
- A Nerd Font (recommended) for file icons

## Install

1. Clone into `~/.config/nvim`
2. Open Neovim and install plugins:

```vim
:PlugInstall
```

3. Install LSP servers (per-language) via:

```vim
:Mason
```

## Keybinds

Leader key is `<Space>`.

### Files

- `<leader>e`: toggle Neo-tree

### Search

- `<leader>sg`: grep in project root (LSP root -> git root -> cwd)
- `<leader>sG`: grep in current working directory

### LSP

These are buffer-local and only active once an LSP attaches.

- `gr`: references
- `gi`: implementation

### Diagnostics

- `]w` / `[w`: next/prev warning
- `]e` / `[e`: next/prev error

### Pane Navigation

- `<C-h>`: move to left pane
- `<C-j>`: move to below pane
- `<C-k>`: move to above pane
- `<C-l>`: move to right pane

### Buffer Navigation

- `<S-h>`: previous buffer
- `<S-l>`: next buffer

### Llama

- Visual mode: select a range, then `<leader>lli` to run `:LlamaInstruct`
- See `:help llama.vim` (and `g:llama_config` in `init.lua`) for the rest of the default mappings.
