# Technical Guides

This directory contains HowTo articles and technical documentation for research tools and systems.

---

## Guides Index

### Development Environment
| Guide | Description |
|-------|-------------|
| [Tmux](tmux.md) | Terminal multiplexer setup and usage |
| [Linux Kernel Development](linux-kernel-dev.md) | Compiling and debugging the Linux kernel |
| [Performance Mode](performance-mode.md) | Disable power management for consistent benchmarking |

### Virtualization & Emulation
| Guide | Description |
|-------|-------------|
| [Device Passthrough](dev-passthrough.md) | Pass PCIe devices to QEMU VMs |
| [QEMU Scripts](../05-infrastructure/qemu/) | Scripts for running QEMU/FEMU VMs |

### Cloud Resources
| Guide | Description |
|-------|-------------|
| [CloudLab](cloudlab.md) | Getting started with CloudLab |

### Research Tools
| Guide | Description |
|-------|-------------|
| [Plotting](plotting.md) | Guidelines for scientific graphs with gnuplot |

### System Administration
| Guide | Description |
|-------|-------------|
| [OS Security Settings](os-security-settings.md) | VT security compliance for Linux machines |

---

## Contributing

When adding a new technical guide, please follow this template:

```markdown
# [Topic] Guide

## Overview
Brief description of what this guide covers.

## Prerequisites
- Required software/access
- Prior knowledge needed

## Quick Reference
TL;DR commands for experienced users.

## Step-by-Step Instructions
Detailed walkthrough...

## Troubleshooting
Common issues and solutions.

## References
- External links

## Changelog
- YYYY-MM-DD: Description by @username
```

---

## Suggestions for New Guides

If you figure out something useful that's not documented here, please add it! Some ideas:

- GDB + QEMU kernel debugging
- Kernel function tracing (ftrace)
- Setting up development VMs
- fio benchmarking best practices
- CXL device testing procedures
