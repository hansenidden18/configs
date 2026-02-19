# Tmux Guide

Tmux is a powerful terminal multiplexer that all students in MoatLab are expected to master. It will save tons of your research time and boost your productivity!

---

## Overview

Tmux allows you to:
- Run multiple terminal sessions in one window
- Detach and re-attach sessions (keeps processes running when you disconnect)
- Split your terminal into panes
- Share terminal sessions with others

---

## Quick Start

### Installation

```bash
# Ubuntu/Debian
sudo apt install tmux

# macOS
brew install tmux
```

### Using the Group Configuration

We have a pre-configured tmux setup. To use it:

```bash
# Apply the terminfo file
tic tmux-256color.terminfo

# Copy the config to your home directory
cp tmux.conf ~/.tmux.conf

# Install Tmux Plugin Manager (TPM)
git clone https://github.com/tmux-plugins/tpm ~/.tmux/plugins/tpm

# Reload tmux config
tmux source ~/.tmux.conf
```

Configuration files:
- [tmux.conf](tmux.conf) - Main configuration
- [tmux-256color.terminfo](tmux-256color.terminfo) - Terminal info for colors

---

## Basic Usage

### Session Management

```bash
# Create a new session
tmux new-session -s mysession

# List all sessions
tmux ls

# Attach to a session
tmux attach -t mysession

# Detach from current session (while inside tmux)
# Press: Ctrl+Space, then d
```

### Window/Pane Management

Using our configuration (prefix is `Ctrl+Space`):

| Action | Keys |
|--------|------|
| Vertical split | `Ctrl+Space`, then `-` |
| Horizontal split | `Ctrl+Space`, then `Shift+\|` |
| Resize pane | `Ctrl+Space`, then `Shift+H/J/K/L` |
| Navigate panes | `Ctrl+Space`, then arrow keys |
| Detach session | `Ctrl+Space`, then `d` |

---

## Recommended Workflow

1. **SSH into server** and start tmux:
   ```bash
   ssh user@server
   tmux new -s research
   ```

2. **Split into panes** for different tasks:
   - One pane for editing
   - One pane for compiling/running
   - One pane for monitoring

3. **Detach when done** (`Ctrl+Space`, `d`) - your processes keep running!

4. **Re-attach later**:
   ```bash
   ssh user@server
   tmux attach -t research
   ```

---

## Troubleshooting

### Colors not working
Run the terminfo fix:
```bash
tic tmux-256color.terminfo
```

### Plugins not loading
Install TPM and press `Ctrl+Space`, then `I` to install plugins.

### Session lost after server reboot
Tmux sessions don't survive reboots. Consider using `tmux-resurrect` plugin for persistence.

---

## References

- [Tmux Cheat Sheet](https://tmuxcheatsheet.com/)
- [Tmux Plugin Manager](https://github.com/tmux-plugins/tpm)
- Check `tmux.conf` for all custom key bindings
