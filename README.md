# ubuntu-chinese-ime

<div align="center">

![ubuntu-chinese-ime](assets/banner.svg)

</div>

<p align="center">

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![OpenClaw](https://img.shields.io/badge/OpenClaw-Supported-blueviolet)](https://github.com/openclaw)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Compatible-green)](https://claude.ai)
[![Codex](https://img.shields.io/badge/Codex-Compatible-orange)](https://github.com)
[![Hermes](https://img.shields.io/badge/Hermes-Agent-blue)](https://github.com)

</p>

<div align="center">

# ubuntu-chinese-ime

Ubuntu / WSL fcitx5 中文输入法安装配置指南

</div>

---

## 核心特性

| 特性 | 说明 |
|------|------|
| 🌙 **fcitx5** | 现代化中文输入法框架，体验接近搜狗/百度 |
| ☁️ **云拼音** | 联想、纠错、云端词库功能齐全 |
| 🔧 **开箱即用** | 一键安装，配置简单 |

---

## 快速开始

```bash
# 安装
sudo apt update
sudo apt install fcitx5 fcitx5-pinyin fcitx5-chinese-addons

# 配置环境变量
cat >> ~/.bashrc << 'EOF'
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
EOF
source ~/.bashrc

# 配置输入法
im-config -n fcitx5
fcitx5-configtool
```

---

## 触发条件

- ubuntu 中文输入法
- ubuntu 安装 fcitx5
- wsl 中文输入
- fcitx5 安装

---

## 快捷键

| 快捷键 | 功能 |
|--------|------|
| `Ctrl + Space` | 激活/关闭输入法 |
| `Shift` | 中英文切换 |
| `Ctrl + Shift` | 切换不同输入法 |

---

## 平台支持

| 平台 | 状态 | 安装方式 |
|------|------|---------|
| OpenClaw | ✅ 支持 | `clawhub install ubuntu-chinese-ime` |
| Claude Code | ✅ 支持 | 复制 SKILL.md 到 `~/claude/skills/ubuntu-chinese-ime/` |
| Codex | ✅ 支持 | 复制 SKILL.md 到 `~/.codex/skills/ubuntu-chinese-ime/` |
| Hermes | ✅ 支持 | 复制 SKILL.md 到 `~/.hermes/skills/ubuntu-chinese-ime/` |

---

## 详见

完整的 SKILL.md 定义和踩坑记录请查阅 [SKILL.md](SKILL.md)。

---

<div align="center">

MIT License © [relunctance](https://github.com/relunctance)

</div>
