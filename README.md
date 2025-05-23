# Base64MCP

一个使用 FastMCP 实现的 Base64 编码和解码工具。本项目展示了如何使用 uv 打包一个 MCP 服务，上传到 PyPI，并通过 uvx 运行。

## 项目介绍

Base64MCP 是一个简单的 MCP (Message Control Protocol) 服务，提供了两个主要功能：

1. **编码 (encode)**: 将字符串转换为 Base64 编码
2. **解码 (decode)**: 将 Base64 编码转换回原始字符串

服务可以通过环境变量配置，将结果转换为大写或小写。

## 安装

### 使用 pip 安装

```bash
pip install base64mcp
```

### 使用 uv 安装

```bash
uv pip install base64mcp
```

## 使用方法

### 设置环境变量

在运行服务前，需要设置以下环境变量：

- `TO_LOW`: 设置为 "true" 将结果转换为小写
- `TO_UPPER`: 设置为 "true" 将结果转换为大写

如果两个变量都设置为 "true"，则 `TO_LOW` 优先。

### 命令行运行

```bash
# 设置环境变量
export TO_LOW=true
export TO_UPPER=false

# 运行服务
base64mcp
```

### 使用 uvx 运行

```bash
# 设置环境变量
export TO_LOW=true
export TO_UPPER=false

# 使用 uvx 运行
uvx base64mcp
```

## 使用 uv 打包 MCP 服务的步骤

以下是使用 uv 打包 MCP 服务并上传到 PyPI 的完整步骤：

### 1. 准备项目结构

创建一个标准的 Python 包结构：

```
mcp-example/
├── pyproject.toml
├── src/
│   └── base64mcp/
│       ├── __init__.py
│       ├── main.py
│       └── server.py
```

### 2. 配置 pyproject.toml

创建一个 `pyproject.toml` 文件，包含以下内容：

```toml
[build-system]
requires = ["setuptools>=61.0", "wheel"]
build-backend = "setuptools.build_meta"
backend-path = ["."]

[project]
name = "base64mcp"
version = "0.1.1"
description = "一个使用 FastMCP 实现的 Base64 编码和解码工具。"

authors = [
    { name = "your_name", email = "your_email@example.com" },
]

requires-python = ">=3.8"
license = { text = "MIT" }

dependencies = [
    "mcp[cli]>=1.9.1",
    "wheel>=0.45.1",
]

# 详细分类，有助于在 PyPI 上被发现
classifiers = [
    "Development Status :: 3 - Alpha",
    "Intended Audience :: Developers",
    "License :: OSI Approved :: MIT License",
    "Programming Language :: Python :: 3",
    "Programming Language :: Python :: 3.8",
    "Programming Language :: Python :: 3.9",
    "Programming Language :: Python :: 3.10",
    "Programming Language :: Python :: 3.11",
    "Programming Language :: Python :: 3.12",
    "Topic :: Software Development :: Libraries :: Python Modules",
    "Topic :: Utilities",
]

# 项目关键词
keywords = ["base64", "mcp", "cli", "tool"]

[project.urls]
Homepage = "https://github.com/yourusername/base64-mcp-tool"
Repository = "https://github.com/yourusername/base64-mcp-tool"

# 定义命令行脚本
[project.scripts]
base64mcp = "base64mcp.main:main_cli"
```

### 3. 安装 uv

如果尚未安装 uv，请先安装：

```bash
pip install uv
```

### 4. 创建虚拟环境并安装依赖

```bash
# 创建虚拟环境
uv venv

# 激活虚拟环境
source .venv/bin/activate  # Linux/macOS
# 或
.venv\Scripts\activate     # Windows

# 安装依赖
uv pip install -e .
```

### 5. 构建包

```bash
# 构建包
uv pip build
```

这将在 `dist/` 目录下创建 wheel 和 tar.gz 文件。

### 6. 上传到 PyPI

首先，确保你已经在 PyPI 上注册了账号，并创建了 API 令牌。

```bash
# 安装 twine
uv pip install twine

# 上传到 PyPI
twine upload dist/*
```

或者使用 uv 直接上传：

```bash
uv pip publish
```

### 7. 使用 uvx 运行

一旦包被上传到 PyPI，你可以使用 uvx 直接运行它：

```bash
# 设置环境变量
export TO_LOW=true
export TO_UPPER=false

# 使用 uvx 运行
uvx base64mcp
```

## 开发

### 本地测试

```bash
# 克隆仓库
git clone https://github.com/yourusername/base64-mcp-tool.git
cd base64-mcp-tool

# 创建虚拟环境
uv venv

# 激活虚拟环境
source .venv/bin/activate  # Linux/macOS
# 或
.venv\Scripts\activate     # Windows

# 安装开发依赖
uv pip install -e .

# 设置环境变量
export TO_LOW=true
export TO_UPPER=false

# 运行服务
python -m base64mcp.main
```

## 许可证

MIT