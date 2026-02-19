# CCC - Claude Code Configuration (Huaicheng's Example Setup)

A collection of custom utilities, configurations, and extensions for Claude Code, the Anthropic CLI tool for AI-assisted coding.

## Quick Start

```bash
# 1. Clone or copy this directory
cp -r ccc/ ~/.claude-custom/

# 2. Install the scripts (ensure ~/bin is in your PATH)
mkdir -p ~/bin
ln -s ~/.claude-custom/bin/ccd ~/bin/ccd
ln -s ~/.claude-custom/bin/cc-export-session ~/bin/cc-export-session

# 3. Copy configuration
cp -r ~/.claude-custom/config/* ~/.claude/

# 4. Copy custom skills (optional)
cp -r ~/.claude-custom/skills/* ~/.claude/skills/

# 5. Copy custom agents (optional)
cp -r ~/.claude-custom/agents/* ~/.claude/agents/
```

## Directory Structure

```
ccc/
├── bin/                    # Utility scripts
│   ├── ccd                 # Session logging wrapper
│   └── cc-export-session   # Session exporter
├── config/                 # Configuration files
│   ├── CLAUDE.md           # Global instructions
│   ├── settings.json       # Main settings
│   └── settings.local.json # Local overrides
├── skills/                 # Custom skills
│   └── planning-with-files/
└── agents/                 # Custom agents (example)
    └── test-writer.md      # Example agent
```

## Components

### Scripts (`bin/`)

#### `ccd` - Session Logging Wrapper

A bash wrapper that runs Claude Code with automatic session logging to markdown.

> **WARNING**: `ccd` runs with `--dangerously-skip-permissions`, which bypasses all confirmation prompts. Claude can execute commands, modify files, and make system changes without asking. Use with caution - this removes the human-in-the-loop safety check and may cause unintended damage.

**Usage:**
```bash
ccd [claude arguments...]
ccd                           # Start session in current directory
ccd --model opus              # Use specific model
```

**Features:**
- Skips permission prompts (`--dangerously-skip-permissions`)
- Automatically exports session to markdown after completion
- Appends to `~/.claude/my-session-logs/cc-project-<path>.md`
- Creates symlink `./cc-session.md` in the working directory
- Captures thinking blocks in the export

#### `cc-export-session` - Session Exporter

A Python tool to export Claude Code session JSONL files to readable markdown.

**Usage:**
```bash
# List all sessions (newest first)
cc-export-session --list

# Export specific session to stdout
cc-export-session /path/to/session.jsonl

# Export to file
cc-export-session /path/to/session.jsonl -o output.md

# Export ALL sessions to ~/claude-exports/
cc-export-session --all
```

**Output Format:**
- `## User` - User messages
- `## Assistant` - Assistant responses
- `## Assistant (Thinking)` - Internal reasoning
- `## Assistant (Tool: <name>)` - Tool invocations with summaries

### Configuration (`config/`)

#### `CLAUDE.md` - Global Instructions

Concise guidelines for Claude Code covering:
- Shell scripts and process management
- Code style (C/C++, Python, Rust)
- Git commits and whitespace rules
- Academic writing conventions
- Linux kernel development basics

**Note:** Customize for your own workflow.

#### `settings.json` - Main Settings

Configures Claude Code with:
- Default permission mode
- Custom status line (via `ccstatusline`)
- Enabled plugins

**Required Plugins:**
Install these via Claude Code's plugin system:
```
feature-dev@claude-plugins-official
code-review@claude-plugins-official
playwright@claude-plugins-official
document-skills@anthropic-agent-skills
```

### Custom Skills (`skills/`)

#### `planning-with-files/`
Manus-style persistent markdown files for:
- Task planning
- Progress tracking
- Knowledge storage

### Custom Agents (`agents/`)

#### `test-writer.md`
Example agent for test generation.

Create your own agents by adding `.md` files to `~/.claude/agents/`.

## Session Storage Locations

| Type | Location |
|------|----------|
| Raw JSONL | `~/.claude/projects/<project-path>/*.jsonl` |
| Exported MD (ccd) | `~/.claude/my-session-logs/` |
| Bulk exports | `~/claude-exports/` |

## Installation Options

### Option 1: Symlinks (Recommended)
Keep configs in this repo and symlink to `~/.claude/`:
```bash
ln -s /path/to/ccc/config/CLAUDE.md ~/.claude/CLAUDE.md
ln -s /path/to/ccc/config/settings.json ~/.claude/settings.json
# ... etc
```

### Option 2: Copy
Copy all files directly to `~/.claude/` (may diverge from source).

### Option 3: Selective
Pick only the components you need.

## Customization

### CLAUDE.md
Key sections to customize:
- Code style preferences
- Shell script conventions

### Settings
Adjust `settings.json` for:
- Different permission modes
- Different plugins
- Status line configuration

## Requirements

- Claude Code CLI installed
- Python 3.6+ (for `cc-export-session`)
- Node.js (for status line via `ccstatusline`)

## License

Personal utilities - use and modify as needed.
