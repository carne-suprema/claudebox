# ClaudeBox 🐳

[![Docker](https://img.shields.io/badge/Docker-Required-blue.svg)](https://www.docker.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![GitHub](https://img.shields.io/badge/GitHub-RchGrav%2Fclaudebox-blue.svg)](https://github.com/RchGrav/claudebox)

The Ultimate Claude Code Docker Development Environment - Run Claude AI's coding assistant in a fully containerized, reproducible environment with pre-configured development profiles and MCP servers.

```bash
 ██████╗██╗      █████╗ ██╗   ██╗██████╗ ███████╗
██╔════╝██║     ██╔══██╗██║   ██║██╔══██╗██╔════╝
██║     ██║     ███████║██║   ██║██║  ██║█████╗
██║     ██║     ██╔══██║██║   ██║██║  ██║██╔══╝
╚██████╗███████╗██║  ██║╚██████╔╝██████╔╝███████╗
 ╚═════╝╚══════╝╚═╝  ╚═╝ ╚═════╝ ╚═════╝ ╚══════╝

██████╗  ██████╗ ██╗  ██╗
██╔══██╗██╔═══██╗╚██╗██╔╝
██████╔╝██║   ██║ ╚███╔╝ 
██╔══██╗██║   ██║ ██╔██╗ 
██████╔╝╚██████╔╝██╔╝ ██╗
╚═════╝  ╚═════╝ ╚═╝  ╚═╝
```

## 🚀 What's New in Latest Update

- **Five MCP Servers**: Sequential Thinking, Memory, Context7, Task Master AI, and Playwright servers included
- **macOS Compatibility**: Full support for macOS with proper command compatibility
- **Python Profile Fixed**: Python development now includes proper Python3, pip, venv, and uv package manager
- **Improved PATH Handling**: Development tools (like uv, python3) now properly accessible in all modes
- **Better Profile Management**: Profile commands now exit cleanly after setup instead of launching Claude
- **Enhanced Flag Separation**: Better handling of ClaudeBox vs Claude Code specific flags
- **Shell Mode Improvements**: Fixed shell mode functionality with proper environment setup
- **Git Authentication**: SSH key mounting for Git operations (works best with SSH host aliases)
- **Development-Friendly Defaults**: Sudo enabled by default for productivity

## ✨ Features

- **Containerized Environment**: Run Claude Code in an isolated Docker container
- **Five MCP Servers**: Pre-configured Sequential Thinking, Memory, Context7, Task Master AI, and Playwright servers
- **Development Profiles**: Pre-configured language stacks (C/C++, Python, Rust, Go, etc.) with proper tool integration
- **Multi-Project Support**: Each repository gets its own isolated container configuration and profiles
- **Git Integration**: Automatic SSH key mounting for Git authentication (works with SSH host aliases)
- **Persistent Configuration**: Settings and data persist between sessions
- **Package Management**: Easy installation of additional development tools
- **Auto-Setup**: Handles Docker installation and configuration automatically
- **Development-Friendly Defaults**: Sudo enabled by default for development productivity
- **Cross-Platform**: Works on Linux and macOS (WSL2 for Windows)

## 📋 Prerequisites

- Linux or macOS (WSL2 for Windows)
- Bash shell
- Docker (will be installed automatically if missing)

## 🛠️ Installation

```bash
# Download and setup ClaudeBox
curl -O https://raw.githubusercontent.com/RchGrav/claudebox/main/claudebox
chmod +x claudebox

# Run initial setup (handles everything automatically)
./claudebox
```

The script will:

- ✅ Check for Docker (install if needed)
- ✅ Configure Docker for non-root usage
- ✅ Build the ClaudeBox image with MCP servers
- ✅ Create a global symlink for easy access
- ✅ Set up MCP configuration in your workspace

## 📚 Usage

### Basic Usage

```bash
# Launch Claude CLI with MCP servers enabled
claudebox

# Pass arguments to Claude
claudebox --model opus -c

# Get help
claudebox help          # ClaudeBox specific help
claudebox --help        # Claude CLI help
```

### Development Profiles

ClaudeBox includes 15+ pre-configured development environments:

```bash
# List all available profiles
claudebox profile

# Install specific profiles (exits after setup)
claudebox profile python ml        # Python + Machine Learning
claudebox profile c openwrt       # C/C++ + OpenWRT
claudebox profile rust go         # Rust + Go

# Then launch Claude with your profiles active
claudebox
```

#### Available Profiles

**Fully Implemented:**

- **c** - C/C++ Development (gcc, g++, gdb, valgrind, cmake, cmocka, lcov, ncurses)
- **openwrt** - OpenWRT Development (cross-compilation, QEMU, build essentials)
- **rust** - Rust Development (cargo, rustc, clippy, rust-analyzer)
- **python** - Python Development (python3, pip, venv, plus global uv package manager)
- **go** - Go Development (Go 1.21.5 toolchain)
- **javascript** - Node.js/TypeScript development tools

**Coming Soon (not yet in cached build):**

- **java** - Java Development (OpenJDK 17, Maven, Gradle, Ant)
- **ruby** - Ruby Development (Ruby, gems, bundler)
- **php** - PHP Development (PHP, Composer, common extensions)
- **database** - Database Tools (PostgreSQL, MySQL, SQLite, Redis, MongoDB clients)
- **devops** - DevOps Tools (Docker, Kubernetes, Terraform, Ansible, AWS CLI)
- **web** - Web Development (nginx, curl, httpie, jq)
- **embedded** - Embedded Development (ARM toolchain, OpenOCD, PlatformIO)
- **datascience** - Data Science (NumPy, Pandas, Jupyter, R)
- **security** - Security Tools (nmap, tcpdump, wireshark, penetration testing)
- **ml** - Machine Learning (PyTorch, TensorFlow, scikit-learn, transformers)

### MCP Servers

ClaudeBox includes five powerful MCP servers:

1. **Sequential Thinking Server** - For complex problem-solving with revision capabilities
2. **Memory Server** - Knowledge graph for persistent memory across sessions
3. **Context7** - Upstash context management and caching capabilities
4. **Task Master AI** - Advanced project management and task tracking capabilities
5. **Playwright** - Browser automation and web testing tools

These are automatically configured and available to Claude within the container.

### Multi-Project Support

ClaudeBox supports running multiple instances with different profiles across different repositories:

```bash
# Repository 1: Python web development
cd ~/projects/django-app
claudebox profile python ml
claudebox  # Runs with Python + ML tools

# Repository 2: C++ systems programming  
cd ~/projects/cpp-engine
claudebox profile c rust
claudebox  # Runs with C/C++ + Rust tools

# Repository 3: OpenWRT embedded development
cd ~/projects/router-firmware
claudebox profile c openwrt
claudebox  # Runs with cross-compilation tools
```

Each project directory maintains its own:

- Container configuration and profiles
- Development tool installations
- Virtual environments (for Python projects)

### Package Management

```bash
# Install additional packages
claudebox install htop vim tmux

# Open a shell in the container
claudebox shell

# Update Claude CLI
claudebox update
```

### Git Authentication

ClaudeBox automatically mounts your SSH keys and Git configuration for seamless Git operations:

#### SSH Keys with Host Aliases (Recommended)

```bash
# Ensure your ~/.ssh/config has host aliases like:
# Host github.com-mykey
#   HostName github.com
#   User git
#   IdentityFile ~/.ssh/my_key

# Clone/set remote using the host alias
git clone github.com-mykey:username/repo.git
# or
git remote set-url origin github.com-mykey:username/repo.git

claudebox shell
ssh -T github.com-mykey  # Should show GitHub greeting
git push origin main  # Works with SSH key authentication and your Git config
```

**Git Configuration**: ClaudeBox automatically detects and configures your Git user name and email from the host system, ensuring commits have the correct author information regardless of repository.

### Security Options

**Current Defaults (Development-Friendly):**

- Sudo access: **ENABLED** by default
- Permission checks: **SKIPPED** by default

```bash
# To enable stricter security, modify these variables in the script:
# CLAUDEBOX_ENABLE_SUDO=false        # Disable sudo
# Comment out: DEFAULT_FLAGS+=("--dangerously-skip-permissions")
```

### Maintenance

```bash
# Remove ClaudeBox image
claudebox clean

# Deep clean (remove all build cache)
claudebox clean --all

# Rebuild the image from scratch
claudebox rebuild
```

## 🔧 Configuration

ClaudeBox stores data in:

- `~/.claude/` - Claude configuration and data
- `~/.claudebox/` - ClaudeBox-specific data (MCP memory, etc.)
- Current directory mounted as `/workspace` in container

### Environment Variables

- `ANTHROPIC_API_KEY` - Your Anthropic API key
- `NODE_ENV` - Node environment (default: production)

### MCP Configuration

ClaudeBox automatically sets up `.mcp.json` in your workspace with all five MCP servers configured and ready to use.

## 🏗️ Architecture

ClaudeBox creates a Debian-based Docker image with:

- Node.js (via NVM for version flexibility)
- Claude Code CLI (@anthropic-ai/claude-code)
- Five MCP servers (Sequential Thinking, Memory, Context7, Task Master AI, Playwright)
- User account matching host UID/GID
- Volume mounts for workspace and configuration
- Ephemeral containers with persistent data directories

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📝 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🐛 Troubleshooting

### Docker Permission Issues

ClaudeBox automatically handles Docker setup, but if you encounter issues:

1. The script will add you to the docker group
2. You may need to log out/in or run `newgrp docker`
3. Run `claudebox` again

### MCP Servers Not Working

Test MCP servers after installation:

```bash
claudebox shell
~/test-mcp.sh
```

### Profile Installation Failed

```bash
claudebox clean --all
claudebox rebuild
claudebox profile <name>
```

### Can't Find Command

ClaudeBox creates a symlink in your user's local bin directory:

```bash
# Check if symlink exists
ls -la ~/.local/bin/claudebox

# If missing, the script will recreate it on next run
./claudebox
```

### Python Tools Not Found (uv, python3)

If development tools aren't available after installing the Python profile:

```bash
# Rebuild with fresh profile
claudebox clean --all
claudebox profile python
claudebox shell
which python3 uv  # Should now work
```

### macOS Compatibility Issues

ClaudeBox now fully supports macOS. If you encounter issues:

```bash
# Ensure script is executable
chmod +x claudebox

# Clean and rebuild if needed
./claudebox clean --all
./claudebox profile <your-profiles>
```

### Git Authentication Issues

If Git push/pull operations fail:

```bash
# Check SSH key permissions on host
ls -la ~/.ssh/
chmod 600 ~/.ssh/id_* ~/.ssh/*_rsa ~/.ssh/*_ed25519  # Fix key permissions
chmod 644 ~/.ssh/*.pub  # Fix public key permissions

# Test SSH connection using host alias
claudebox shell
ssh -T github.com-youralias  # Should show GitHub greeting

# If using direct github.com, ensure key is specified
ssh -T -i ~/.ssh/your_key git@github.com

# Set up proper remote URL with host alias
git remote set-url origin github.com-youralias:username/repo.git

# Alternative: Use GitHub CLI
claudebox shell
gh auth login --web
```

## 🎉 Acknowledgments

- [Anthropic](https://www.anthropic.com/) for Claude AI
- [Model Context Protocol](https://github.com/anthropics/model-context-protocol) for MCP servers
- Docker community for containerization tools
- All the open-source projects included in the profiles

---

Made with ❤️ for developers who love clean, reproducible environments

## Contact

**Author/Maintainer:** RchGrav  
**GitHub:** [@RchGrav](https://github.com/RchGrav)
