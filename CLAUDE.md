# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

ClaudeBox is a Docker-based development environment that runs Claude Code CLI in an isolated, reproducible container with pre-configured MCP servers and development tools. It provides 15+ development profiles (C/C++, Python, Rust, Go, etc.) and includes built-in security features like network firewalls.

## Core Architecture

- **Single executable script**: `claudebox` - Bash script (~1400 lines) that handles everything
- **Docker-based**: Creates Debian bookworm containers with development tools
- **Profile system**: Modular installation of language stacks stored in `~/.claudebox/profiles/`
- **Project-specific isolation**: Each project gets its own container configuration and data
- **MCP integration**: Pre-configured with Sequential Thinking, Memory, Task Master AI, and Playwright servers
- **Development-focused**: Network firewall disabled and sudo enabled by default for ease of development

## Key Commands

### Development
```bash
# Basic usage
./claudebox                           # Launch Claude CLI in container
./claudebox --help                    # Show all options

# Development profiles
./claudebox profile                   # List available profiles
./claudebox profile c python rust    # Install multiple profiles
./claudebox install htop vim tmux     # Install additional packages

# Shell access
./claudebox shell                     # Open interactive shell in container
```

### Maintenance
```bash
# Clean up
./claudebox clean                     # Remove containers (preserve image)
./claudebox clean --all               # Complete cleanup
./claudebox clean --project           # Remove only current project data
./claudebox rebuild                   # Force rebuild from scratch

# Status
./claudebox info                      # Show profile status and containers
```

## Development Profiles

Each profile installs specific tools and languages:
- **c**: GCC, GDB, Valgrind, CMake, CMocka, coverage tools
- **python**: Python3, pip, venv, and `uv` package manager with proper PATH setup
- **rust**: Rustup, Cargo, Clippy
- **go**: Latest Go toolchain
- **openwrt**: Cross-compilation tools, QEMU emulation
- **ml**: Machine learning libraries (PyTorch, TensorFlow)

## Project Structure

- `claudebox` - Main executable script containing all logic
- `README.md` - User documentation
- `LICENSE` - MIT license

## Configuration Files

### Profile Storage
- `~/.claudebox/profiles/<project-hash>.ini` - Per-project profile configuration
- `~/.claudebox/.mcp.json` - Global MCP server configuration
- `~/.claudebox/<project>/firewall/allowlist` - Project-specific network allowlist

### Container Behavior
- Project directory mounted as `/workspace`
- User data persists in `~/.claudebox/` and `~/.claude/`
- Each project gets isolated container with specific tools

## Security Model

### Network Firewall
- Default: Disabled for ease of development (`CLAUDEBOX_DISABLE_FIREWALL=true`)
- Can be enabled with `CLAUDEBOX_DISABLE_FIREWALL=false` 
- Project allowlists in `firewall/allowlist` files when enabled
- Anthropic APIs always allowed when firewall is active

### Privilege Model
- Containers run as non-root by default
- Sudo enabled by default (`CLAUDEBOX_ENABLE_SUDO=true`)
- Can be disabled with `CLAUDEBOX_ENABLE_SUDO=false`
- Docker capabilities: `NET_ADMIN`, `NET_RAW` for firewall functionality

## Development Patterns

1. **Profile-based development**: Install language profiles before coding
2. **Project isolation**: Each directory gets separate container configuration
3. **Persistent tooling**: Profiles tracked and automatically installed on container creation
4. **Development-friendly**: Firewall disabled and sudo enabled by default for productivity

## Important Implementation Details

- Uses `docker run --rm` for ephemeral containers
- Dockerfile generated dynamically based on active profiles
- Profile changes trigger automatic image rebuilds
- User/group IDs matched between host and container
- MCP servers configured globally but used per-project

## Testing

No automated test suite - manual testing via profile installation and container creation.