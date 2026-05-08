---
name: ubuntu-chinese-ime
description: Ubuntu/WSL 安装 fcitx5 中文输入法，解决中文输入问题
description_en: Install fcitx5 Chinese IME on Ubuntu/WSL to enable Chinese input
triggers:
  - ubuntu 中文输入法
  - ubuntu 安装 fcitx5
  - ubuntu 安装 中文输入
  - wsl 中文输入
  - linux 输入法
  - fcitx5 安装
  - ubuntu chinese input method
  - install fcitx5
category: devops
author: relunctance
created: 2026-05-08
updated: 2026-05-08
tags:
  - ubuntu
  - wsl
  - fcitx5
  - 中文输入
  - fcitx5-pinyin
  - fcitx5-chinese-addons
platforms:
  openclaw: true
  claude_code: true
  hermes: true
---

# ubuntu-chinese-ime

## 概述

Ubuntu / WSL Ubuntu 桌面版安装配置 fcitx5 中文输入法。

推荐组合：`fcitx5 + fcitx5-pinyin + fcitx5-chinese-addons`（云拼音、联想、纠错功能齐全，体验接近搜狗/百度）

## 踩坑记录（必看）

| 坑 | 解决方案 |
|---|---|
| WSLg / RDP 桌面里 fcitx5 启动后立即退出 | 添加 `--disable waylandim` 参数禁用 Wayland 输入法模块 |
| mstsc 连 Ubuntu 桌面后 Chrome 无法中文 | Chromium .desktop 文件的 `Exec=` 里要加 `GTK_IM_MODULE=fcitx QT_IM_MODULE=fcitx XMODIFIERS=@im=fcitx` |
| 右上角面板没有输入法图标 | fcitx5 在运行即可（ GNOME 不加载托盘插件），直接用 Ctrl+Space 切换 |
| 环境变量没有生效 | 确保在 `~/.bashrc` 里配置，并 `source ~/.bashrc` |

## 快速安装

### 1. 安装

```bash
sudo apt update
sudo apt install fcitx5 fcitx5-pinyin fcitx5-chinese-addons
```

### 2. 环境变量

```bash
cat >> ~/.bashrc << 'EOF'
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
EOF

source ~/.bashrc
```

### 3. 配置输入法（无需图形界面操作）

```bash
im-config -n fcitx5
```

### 4. 启动 fcitx5

WSLg / RDP / mstsc 桌面环境，用 systemd user service 管理：

```bash
mkdir -p ~/.config/systemd/user

cat > ~/.config/systemd/user/fcitx5.service << 'EOF'
[Unit]
Description=Fcitx5 Input Method
After=display-manager.service

[Service]
Environment=DISPLAY=:0
Environment=GTK_IM_MODULE=fcitx
Environment=QT_IM_MODULE=fcitx
Environment=XMODIFIERS=@im=fcitx
ExecStart=/usr/bin/fcitx5 --disable waylandim
Restart=on-failure
RestartSec=1

[Install]
WantedBy=graphical.target
EOF

systemctl --user daemon-reload
systemctl --user enable --now fcitx5
```

> **关键参数**：`--disable waylandim` —— WSLg 和 RDP 环境下 Wayland compositor 权限不足会导致 fcitx5 启动失败，必须禁用。

### 5. 桌面应用启动脚本加上输入法变量

如果 Chromium / Chrome 在桌面有 `.desktop` 文件，编辑 `Exec=` 行：

```bash
# 找到 desktop 文件路径
# 通常是 ~/Desktop/chromium.desktop 或 ~/.local/share/applications/chromium.desktop

# 在 Exec= 行的最前面加上输入法环境变量：
Exec=env GTK_IM_MODULE=fcitx QT_IM_MODULE=fcitx XMODIFIERS=@im=fcitx chromium-browser %U
```

**验证方法**：关闭浏览器，从终端启动：

```bash
GTK_IM_MODULE=fcitx QT_IM_MODULE=fcitx XMODIFIERS=@im=fcitx chromium-browser
```

### 6. 验证

```bash
# 检查 fcitx5 进程运行中
ps aux | grep fcitx5 | grep -v grep

# 检查当前输入法状态
fcitx5-remote

# 如果输出 0，手动切换到拼音
fcitx5-remote -s pinyin
```

## 常见问题

**Q: fcitx5-remote 显示 0，但右上角没有输入法图标？**
A: GNOME 桌面不显示 fcitx5 托盘图标是正常的，只要进程在运行，Ctrl+Space 就能切换输入法。

**Q: Ctrl+Space 没反应？**
A: 先确认 fcitx5 进程在运行，再确认应用程序的启动命令加了输入法环境变量。

**Q: WSLg 和 mstsc 有什么区别？**
A: WSLg 是 Windows 自带的 WSL 图形支持（自动转发到 Windows X server）；mstsc 是远程桌面。连 mstsc 时 DISPLAY 变量通常设为 `:0`。

## 安装

```bash
# OpenClaw
clawhub install ubuntu-chinese-ime

# Claude Code
mkdir -p ~/claude/skills/ubuntu-chinese-ime
cp SKILL.md ~/claude/skills/ubuntu-chinese-ime/

# Hermes
mkdir -p ~/.hermes/skills/ubuntu-chinese-ime
cp SKILL.md ~/.hermes/skills/ubuntu-chinese-ime/
```
