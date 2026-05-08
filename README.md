# ubuntu-chinese-ime

> Install fcitx5 Chinese IME on Ubuntu / WSL Ubuntu Desktop

## Overview

Install and configure fcitx5 Chinese input method on Ubuntu / WSL Ubuntu Desktop.

Recommended package: `fcitx5 + fcitx5-pinyin + fcitx5-chinese-addons` — includes cloud pinyin, autocomplete, and error correction, comparable to Sogou/Baidu IME experience.

## Triggers

- ubuntu chinese input method
- install fcitx5
- ubuntu 中文输入法
- ubuntu 安装 fcitx5
- wsl 中文输入
- linux input method

## Quick Setup

### Install

```bash
sudo apt update
sudo apt install fcitx5 fcitx5-pinyin fcitx5-chinese-addons
```

### Configure Environment Variables

```bash
cat >> ~/.bashrc << 'EOF'
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
EOF

source ~/.bashrc
```

### Configure Input Method

```bash
im-config -n fcitx5
fcitx5-configtool
```

In the config UI:
1. Ensure `Keyboard - English` is at the top (default English input)
2. Add `Pinyin` or `Chinese - Pinyin (fcitx5-chinese-addons)`

### Verify

```bash
# Check fcitx5 installed
which fcitx5 && fcitx5 --version

# Check env vars
echo $GTK_IM_MODULE   # should output: fcitx

# Start manually if not auto-started
fcitx5 &

# Test: open browser, switch to Chinese IME, type pinyin
```

## Input Method Shortcuts

| Shortcut | Action |
|----------|--------|
| `Ctrl + Space` | Toggle IME on/off |
| `Shift` | Switch Chinese/English |
| `Ctrl + Shift` | Switch between input methods |

## Pitfalls

| Issue | Solution |
|-------|----------|
| IME not working after reboot | Add env vars to `~/.bashrc`, logout and login again |
| im-config ineffective (WSLg) | Manually export the 3 env vars |
| fcitx5 not started | `fcitx5 &` or set to auto-start |
| Sogou IME won't install | Ubuntu 24.04 removed fcitx4, use fcitx5-pinyin instead |
| Baidu IME unavailable on Linux | Use fcitx5-chinese-addons cloud pinyin |

## Installation

### OpenClaw
```bash
clawhub install ubuntu-chinese-ime
```

### Claude Code
```bash
mkdir -p ~/claude/skills/ubuntu-chinese-ime
cp SKILL.md ~/claude/skills/ubuntu-chinese-ime/
```

### Hermes
```bash
mkdir -p ~/.hermes/skills/ubuntu-chinese-ime
cp SKILL.md ~/.hermes/skills/ubuntu-chinese-ime/
```

### Manual (GitHub)
```bash
git clone https://github.com/relunctance/ubuntu-chinese-ime.git
```

## Platforms

| Platform | Status |
|----------|--------|
| OpenClaw | ✅ Supported |
| Claude Code | ✅ Supported |
| Hermes | ✅ Supported |

## See Also

- [中文文档 (Chinese README)](README_zh.md)
