# Neovim Keymaps

Leader key: `<Space>`

## File Explorer (NvimTree)

| Key | Action |
|-----|--------|
| `<leader>e` | Toggle NvimTree |

### Inside NvimTree

| Key | Action |
|-----|--------|
| `S` | Search in directory (grug-far) |
| `P` | Preview file (watch) |
| `<Esc>` | Close preview |
| `<Tab>` | Preview file / expand directory |

## Buffers

| Key | Action |
|-----|--------|
| `<C-h>` | Previous buffer |
| `<C-l>` | Next buffer |
| `<C-j>` | Move buffer left |
| `<C-k>` | Move buffer right |
| `<leader>q` | Close buffer (preserve window layout) |
| `Q` | Close all other tabs/windows |
| `<leader><leader>` | Toggle between last two buffers |

## Window Management

| Key | Action |
|-----|--------|
| `<C-w>%` | Split vertically |
| `<C-w>"` | Split horizontally |
| `<C-w>m` | Maximize window |
| `<C-w>h/j/k/l` | Move to split (tmux-aware) |
| `<C-S-Left/Down/Up/Right>` | Resize split |
| `<leader>H/J/K/L` | Swap buffer in direction |

## Terminal (ToggleTerm)

| Key | Action |
|-----|--------|
| `<C-\>` | Toggle floating terminal |
| `<leader>.f` | Open terminal in current file directory |
| `<leader>.r` | Open terminal in project root |
| `<leader>.h` | Toggle htop |

### Inside terminal

| Key | Action |
|-----|--------|
| `<Esc>` or `<C-[>` | Exit terminal mode |
| `<C-w>` | Exit terminal mode and switch window |

## Search & Find

| Key | Action |
|-----|--------|
| `<leader>ff` | Find files |
| `<leader>fg` | Live grep |
| `<leader>fs` | Grep word under cursor |
| `<leader>fh` | Command history |
| `<leader>f?` | Help tags |
| `<leader>fd` | Diagnostics (LSP) |
| `<leader>S` (n/v) | Find and replace (grug-far) |
| `<leader>w` | Leap forward |
| `<leader>b` | Leap backward |
| `<leader>W` | Leap from window |

### Inside Telescope picker

| Key | Action |
|-----|--------|
| `<C-h>` | Scroll preview left |
| `<C-l>` | Scroll preview right |

## Editing

| Mode | Key | Action |
|------|-----|--------|
| normal | `<leader>j` | Insert blank line below (stay in normal) |
| normal | `<leader>k` | Insert blank line above (stay in normal) |
| normal | `J` | Join lines (keep cursor position) |
| normal | `j` / `k` | Move by visual line (soft-wrap aware) |
| visual | `J` | Move selection down |
| visual | `K` | Move selection up |
| visual | `<` | Dedent (stay in visual) |
| visual | `>` | Indent (stay in visual) |
| insert | `<C-H>` | Delete word (Ctrl-Backspace) |
| insert | `{<CR>` | Auto-complete curly brackets |

## Clipboard

| Mode | Key | Action |
|------|-----|--------|
| n/v | `<leader>y` | Yank to system clipboard |
| normal | `<leader>Y` | Yank line to system clipboard |
| n/v | `<leader>d` | Delete to system clipboard |
| normal | `<leader>cd` | Copy current file directory to clipboard |
| normal | `gx` | Open link under cursor in browser |

## Rename & Replace

| Mode | Key | Action |
|------|-----|--------|
| normal | `<leader>cw` | Rename word under cursor (current file) |
| visual | `<leader>cw` | Rename selection (current file) |
| normal | `<F2>` | LSP rename symbol (across files) |

## LSP

| Key | Action |
|-----|--------|
| `K` | Hover documentation |
| `gd` | Go to definition |
| `gD` | Go to declaration |
| `gt` | Go to type definition |
| `gi` | Go to implementation |
| `gs` | Signature help |
| `gr` | References |
| `gh` | Toggle inlay hints |
| `gl` | Open diagnostic float |
| `[d` | Previous diagnostic |
| `]d` | Next diagnostic |
| `<F3>` | Format buffer |
| `<F4>` | Code action |
| `<leader>tl` | Toggle LSP on/off |

## Completion (nvim-cmp)

| Mode | Key | Action |
|------|-----|--------|
| insert | `<CR>` | Confirm selected item |
| insert | `<C-k>` | Toggle signature help / trigger completion |
| i/s | `<S-Tab>` | Jump to next snippet field |

## Folding

| Key | Action |
|-----|--------|
| `zR` | Open all folds |
| `zM` | Close all folds |

## Search Patterns

| Key | Action |
|-----|--------|
| `/` | Forward search (very magic) |
| `?` | Backward search (very magic) |
| `n` / `N` | Next / prev result (centered) |
| `G` | Go to end of file (centered) |
| `<C-n>` | Next quickfix item |
| `<C-p>` | Previous quickfix item |

## Git

| Mode | Key | Action |
|------|-----|--------|
| normal | `]c` | Next hunk |
| normal | `[c` | Previous hunk |
| n/v | `<leader>gs` | Stage hunk |
| n/v | `<leader>gr` | Reset hunk |
| normal | `<leader>gS` | Stage buffer |
| normal | `<leader>gu` | Undo stage hunk |
| normal | `<leader>gR` | Reset buffer |
| normal | `<leader>gp` | Preview hunk |
| normal | `<leader>gb` | Blame line |
| normal | `<leader>gd` | Diff this |
| normal | `<leader>gD` | Diff against previous commit |
| normal | `<leader>gf` | File git history (DiffView) |
| normal | `<leader>tb` | Toggle current line blame |
| normal | `<leader>td` | Toggle deleted lines |
| o/x | `ih` | Select hunk (text object) |
| normal | `<leader>.g` | Open LazyGit |

## Tools

| Key | Action |
|-----|--------|
| `<leader>u` | Toggle undotree |
| `<leader>?` | Ask Claude (sends current line as prompt) |
| `<leader>./` | Execute current file as script (if has shebang) |

## Compiler Explorer

| Mode | Key | Action |
|------|-----|--------|
| normal | `<leader>ce` | Compile buffer |
| visual | `<leader>ce` | Compile selection |
| normal | `<leader>cl` | Compile live (auto on save) |
| normal | `<leader>ct` | Show instruction tooltip |
| n/v | `<leader>cx` | Open in godbolt.org |

## LaTeX (`.tex` files only)

LocalLeader is `<Space>`.

| Key | Action |
|-----|--------|
| `<localleader>ll` | Compile |
| `<localleader>lk` | Stop compilation |
| `<localleader>lK` | Stop all compilations |
| `<localleader>lc` | Clean auxiliary files |
| `<localleader>lC` | Clean all (including PDF) |
| `<localleader>lv` | View PDF |
| `<localleader>lt` | Toggle TOC |
| `<localleader>li` | Show info |
| `<localleader>ls` | Show status |
| `<localleader>le` | Show errors |
