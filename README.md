---
name: ubuntu-chinese-ime
description: Ubuntu / WSL Ubuntu 安装中文输入法（fcitx5 + pinyin），解决中文输入问题
triggers:
  - ubuntu 中文输入法
  - ubuntu 安装 fcitx5
  - ubuntu 安装 中文输入
  - wsl 中文输入
  - linux 输入法
  - fcitx5 安装
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
---

# ubuntu-chinese-ime

> 在 Ubuntu / WSL Ubuntu 桌面版上安装配置 fcitx5 中文输入法

## 触发条件

用户提到以下任意关键词时使用本 skill：
- `ubuntu 中文输入法`
- `ubuntu 安装 fcitx5`
- `ubuntu 安装 中文输入`
- `wsl 中文输入`
- `linux 输入法`
- `fcitx5 安装`

## 快速执行

### 第一步：安装 fcitx5

```bash
sudo apt update
sudo apt install fcitx5 fcitx5-pinyin fcitx5-chinese-addons
```

### 第二步：配置环境变量

```bash
# 写入 ~/.bashrc
cat >> ~/.bashrc << 'EOF'
# fcitx5 中文输入法
export GTK_IM_MODULE=fcitx
export QT_IM_MODULE=fcitx
export XMODIFIERS=@im=fcitx
EOF

source ~/.bashrc
```

### 第三步：设为默认输入法（可选）

```bash
im-config -n fcitx5
```

### 第四步：重启图形会话

在 Ubuntu 桌面环境注销并重新登录，或者重启。

### 第五步：配置 fcitx5（命令行或图形）

```bash
# 图形方式：应用程序菜单 → fcitx5 Configuration
# 添加拼音输入法：fcitx5-configtool
# 或命令行：
fcitx5-configtool
```

在配置界面：
1. 确保 `Keyboard - English` 在最上面（作为默认英文输入）
2. 添加 `Pinyin` 或 `Chinese - Pinyin (fcitx5-chinese-addons)`

### 第六步：验证

```bash
# 检查 fcitx5 是否运行
ps aux | grep fcitx5

# 如果没有运行，手动启动
fcitx5 &
```

### 切换输入法快捷键

- `Ctrl + Space`：激活/关闭输入法
- `Shift`：中英文切换
- `Ctrl + Shift`：切换不同输入法

## 踩坑记录

| 坑 | 说明 | 解决方案 |
|---|---|---|
| 重启后输入法不生效 | 环境变量未加载 | 加到 `~/.bashrc`，注销重登录 |
| `im-config` 没设对 | WSLg 下可能不生效 | 手动 export 三个环境变量 |
| fcitx5 没启动 | 需手动运行或设置自启 | `fcitx5 &` 或设置自动启动 |
| 搜狗输入法装不上 | Ubuntu 24.04 无 fcitx4 官方支持 | 用 fcitx5-pinyin 替代，体验接近 |
| 百度输入法无 Linux 版 | 百度早已停止维护 | 用 fcitx5-chinese-addons 云拼音替代 |

## 验证步骤

```bash
# 1. 检查 fcitx5 已安装
which fcitx5
fcitx5 --version

# 2. 检查环境变量
echo $GTK_IM_MODULE   # 应输出 fcitx
echo $QT_IM_MODULE    # 应输出 fcitx
echo $XMODIFIERS      # 应输出 @im=fcitx

# 3. 检查 fcitx5 进程
ps aux | grep fcitx5

# 4. 打开任意输入框（Chrome/gedit），切换到中文输入法，输入拼音验证
```

## Ubuntu 24.04 fcitx5 vs 搜狗/百度

| 特性 | fcitx5-pinyin | 搜狗拼音 | 百度拼音 |
|------|---------------|---------|---------|
| 云输入 | ✅ fcitx5-cloudpinyin 模块 | ✅ | ❌ 已停止维护 |
| 模糊音 | ✅ | ✅ | ✅ |
| 联想 | ✅ | ✅ | ✅ |
| 安装难度 | ⭐ apt 一行 | 需第三方源/deb | 无 Linux 版 |
| Ubuntu 24.04 兼容 | ✅ 原生支持 | ❌ fcitx4 已移除 | ❌ |

## WSL 特殊说明

WSL Ubuntu 桌面版使用 WSLg，输入法通过 Wayland/X11 传递：

1. 环境变量必须加到 `~/.bashrc`（WSLg 启动时加载）
2. 注销重登录后生效
3. 如果图形应用看不到输入法，尝试重启 WSL：`wsl --shutdown` 后重新打开
