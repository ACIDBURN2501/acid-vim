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

## Configuration

This config uses environment variables for the `llama.vim` plugin to keep sensitive information out of version control. You need to set these variables:

### Required Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `LLAMA_ENDPOINT_FIM` | URL for fill-in-middle API | `http://localhost:8081/infill` |
| `LLAMA_ENDPOINT_INST` | URL for instruct API | `http://localhost:8081/v1/chat/completions` |
| `LLAMA_MODEL_INST` | Model name for instruct mode | `Devstral-Small-2-24B:Q4_K_M` |
| `LLAMA_MODEL_FIM` | Model name for fill-in-middle mode | `Devstral-Small-2-24B:Q4_K_M` |
| `LLAMA_API_KEY` | API key for authentication | `sk-local` |

### Setup Options

**Option 1: Source .env file (recommended)**

1. Copy the `.env.example` file to `.env`:
   ```bash
   cp .env.example .env
   ```

2. Edit `.env` with your configuration

3. Source it before starting Neovim:
   ```bash
   # In your shell startup file (~/.bashrc, ~/.zshrc, etc.)
   if [ -f "$XDG_CONFIG_HOME/nvim/.env" ]; then
       set -a
       source "$XDG_CONFIG_HOME/nvim/.env"
       set +a
   fi
   ```

**Option 2: Set in shell configuration**

Add these lines to your `~/.bashrc`, `~/.zshrc`, or `~/.profile`:

```bash
export LLAMA_ENDPOINT_FIM="http://your-server:8081/infill"
export LLAMA_ENDPOINT_INST="http://your-server:8081/v1/chat/completions"
export LLAMA_MODEL_INST="YourModelName"
export LLAMA_MODEL_FIM="YourModelName"
export LLAMA_API_KEY="your-api-key"
```

**Option 3: Set temporarily**

```bash
export LLAMA_ENDPOINT_FIM="http://your-server:8081/infill"
export LLAMA_ENDPOINT_INST="http://your-server:8081/v1/chat/completions"
export LLAMA_MODEL_INST="YourModelName"
export LLAMA_MODEL_FIM="YourModelName"
export LLAMA_API_KEY="your-api-key"
nvim
```

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
