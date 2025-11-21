<p align="center">
  <img src="https://raw.githubusercontent.com/haris-musa/excel-mcp-server/main/assets/logo.png" alt="Excel MCP Server Logo" width="300"/>
</p>

[![PyPI version](https://img.shields.io/pypi/v/excel-mcp-server.svg)](https://pypi.org/project/excel-mcp-server/)
[![Total Downloads](https://static.pepy.tech/badge/excel-mcp-server)](https://pepy.tech/project/excel-mcp-server)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![smithery badge](https://smithery.ai/badge/@haris-musa/excel-mcp-server)](https://smithery.ai/server/@haris-musa/excel-mcp-server)
[![Install MCP Server](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/install-mcp?name=excel-mcp-server&config=eyJjb21tYW5kIjoidXZ4IGV4Y2VsLW1jcC1zZXJ2ZXIgc3RkaW8ifQ%3D%3D)

A Model Context Protocol (MCP) server that lets you manipulate Excel files without needing Microsoft Excel installed. Create, read, and modify Excel workbooks with your AI agent.

## Features

- 📊 **Excel Operations**: Create, read, update workbooks and worksheets
- 📈 **Data Manipulation**: Formulas, formatting, charts, pivot tables, and Excel tables
- 🔍 **Data Validation**: Built-in validation for ranges, formulas, and data integrity
- 🎨 **Formatting**: Font styling, colors, borders, alignment, and conditional formatting
- 📋 **Table Operations**: Create and manage Excel tables with custom styling
- 📊 **Chart Creation**: Generate various chart types (line, bar, pie, scatter, etc.)
- 🔄 **Pivot Tables**: Create dynamic pivot tables for data analysis
- 🔧 **Sheet Management**: Copy, rename, delete worksheets with ease
- 🔌 **Triple transport support**: stdio, SSE (deprecated), and streamable HTTP
- 🌐 **Remote & Local**: Works both locally and as a remote service

## Installation

```bash
# 使用 pip 安装
pip install excel-mcp-server-bachstudio

# 或使用 uvx（推荐）
uvx excel-mcp-server-bachstudio stdio
```

### 如果遇到模块导入错误

如果使用 uvx 时遇到 `ModuleNotFoundError`，请清除 uvx 缓存：

```bash
# 清除 uv 缓存
uv cache clean

# 或指定清除特定包
uv cache clean excel-mcp-server-bachstudio
```

## Usage

The server supports three transport methods:

### 1. Stdio Transport (for local use)

```bash
uvx excel-mcp-server-bachstudio stdio
```

```json
{
   "mcpServers": {
      "excel": {
         "command": "uvx",
         "args": ["excel-mcp-server-bachstudio", "stdio"]
      }
   }
}
```

### 2. SSE Transport (Server-Sent Events - Deprecated)

```bash
uvx excel-mcp-server-bachstudio sse
```

**SSE transport connection**:
```json
{
   "mcpServers": {
      "excel": {
         "url": "http://localhost:8000/sse",
      }
   }
}
```

### 3. Streamable HTTP Transport (Recommended for remote connections)

```bash
uvx excel-mcp-server-bachstudio streamable-http
```

**Streamable HTTP transport connection**:
```json
{
   "mcpServers": {
      "excel": {
         "url": "http://localhost:8000/mcp",
      }
   }
}
```

## Environment Variables & File Path Handling

### SSE and Streamable HTTP Transports

When running the server with the **SSE or Streamable HTTP protocols**, you **must set the `EXCEL_FILES_PATH` environment variable on the server side**. This variable tells the server where to read and write Excel files.
- If not set, it defaults to `./excel_files`.

You can also set the `FASTMCP_PORT` environment variable to control the port the server listens on (default is `8017` if not set).
- Example (Windows PowerShell):
  ```powershell
  $env:EXCEL_FILES_PATH="E:\MyExcelFiles"
  $env:FASTMCP_PORT="8007"
  uvx excel-mcp-server-bachstudio streamable-http
  ```
- Example (Linux/macOS):
  ```bash
  EXCEL_FILES_PATH=/path/to/excel_files FASTMCP_PORT=8007 uvx excel-mcp-server-bachstudio streamable-http
  ```

### Stdio Transport

When using the **stdio protocol**, the file path is provided with each tool call, so you do **not** need to set `EXCEL_FILES_PATH` on the server. The server will use the path sent by the client for each operation.

## Available Tools

The server provides a comprehensive set of Excel manipulation tools. See [TOOLS.md](TOOLS.md) for complete documentation of all available tools.

## Credits

本项目基于原项目修改：[haris-musa/excel-mcp-server](https://github.com/haris-musa/excel-mcp-server/tree/v0.1.7)

## License

MIT License - see [LICENSE](LICENSE) for details.
