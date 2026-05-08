# ubuntu-chinese-ime

> Ubuntu / WSL Ubuntu 桌面版安装 fcitx5 中文输入法

## 概述

Ubuntu / WSL Ubuntu 桌面版安装配置 fcitx5 中文输入法。

推荐组合：`fcitx5 + fcitx5-pinyin + fcitx5-chinese-addons`（云拼音、联想、纠错功能齐全，体验接近搜狗/百度输入法）

## 触发条件

- ubuntu 中文输入法
- ubuntu 安装 fcitx5
- ubuntu 安装 中文输入
- wsl 中文输入
- linux 输入法
- fcitx5 安装

## 快速安装

### 安装

```bash
sudo apt update
sudo apt install fcitx5 fcitx5-pinyin fcitx5-chinese-addons
```

### 配置环境变量

```bash
cat >> ~/.bashrc << 'EOF'
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
EOF

source ~/.bashrc
```

### 配置输入法

```bash
im-config -n fcitx5
fcitx5-configtool
```

在配置界面添加 `Pinyin` 输入法，确保 `Keyboard - English` 在最上面作为默认英文输入。

### 验证

```bash
# 检查 fcitx5 已安装
which fcitx5 && fcitx5 --version

# 检查环境变量
echo $GTK_IM_MODULE   # 应输出 fcitx

# 启动（如果没有自动启动）
fcitx5 &

# 测试：打开浏览器输入框，切换到中文输入法，输入拼音验证
```

## 切换输入法快捷键

| 快捷键 | 功能 |
|--------|------|
| `Ctrl + Space` | 激活/关闭输入法 |
| `Shift` | 中英文切换 |
| `Ctrl + Shift` | 切换不同输入法 |

## 踩坑记录

| 坑 | 解决方案 |
|---|---|
| 重启后输入法不生效 | 环境变量加到 `~/.bashrc`，注销重登录 |
| im-config 没设对（WSLg） | 手动 export 三个环境变量 |
| fcitx5 没启动 | `fcitx5 &` 或设置自动启动 |
| 搜狗输入法装不上 | Ubuntu 24.04 无 fcitx4 官方支持，用 fcitx5-pinyin 替代 |
| 百度输入法无 Linux 版 | 用 fcitx5-chinese-addons 云拼音替代 |

## 安装

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

## 平台支持

| 平台 | 状态 |
|------|------|
| OpenClaw | ✅ 支持 |
| Claude Code | ✅ 支持 |
| Hermes | ✅ 支持 |

## 相关文档

- [English README](README.md)
