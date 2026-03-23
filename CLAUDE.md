# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 项目概述

Sunshine 是一个自托管的游戏流媒体主机（Moonlight 的服务端），提供低延迟、云游戏服务器能力。支持 AMD、Intel、Nvidia GPU 硬件编码，也支持软件编码。

## 常用命令

### 构建
```bash
# 创建构建目录（使用 cmake-build- 前缀）
mkdir cmake-build-release
cd cmake-build-release

# 配置项目（Linux/macOS）
cmake ..

# macOS 配置
cmake .. -DCMAKE_BUILD_TYPE=Release

# Windows 配置（使用 msys2 和 ucrt64）
# 需要前缀: C:\msys64\msys2_shell.cmd -defterm -here -no-start -ucrt64 -c

# 编译
cmake --build . -j$(nproc)
```

### 测试
- 测试框架：Google Test (gtest)
- 测试可执行文件：`test_sunshine`，位于构建目录的 `tests/` 子目录中

### 代码风格
- 遵循 `.clang-format` 中的 C/C++ 代码风格指南

## 架构

### 核心模块 (src/)
- **main.cpp**: 程序入口
- **stream.cpp**: 流媒体核心逻辑
- **video.cpp**: 视频编码（支持 NVENC、QuickSync、VAAPI）
- **audio.cpp**: 音频处理
- **input.cpp**: 输入处理（键盘、鼠标、手柄）
- **rtsp.cpp**: RTSP 协议实现
- **nvhttp.cpp**: HTTP 服务器（Web UI）
- **config.cpp**: 配置管理
- **crypto.cpp**: 加密功能
- **process.cpp**: 进程管理

### 平台相关 (src/platform/)
- Linux、macOS、Windows 平台特定实现

### NVIDIA 编码 (src/nvenc/)
- NVIDIA NVENC 硬件编码器相关代码

### 构建系统 (cmake/)
- `cmake/prep/`: 预处理配置（版本、选项、初始化）
- `cmake/dependencies/`: 依赖管理（FFmpeg、Boost、OpenSSL 等）
- `cmake/targets/`: 编译目标定义
- `cmake/packaging/`: 打包配置

### 测试 (tests/)
- Google Test 单元测试
