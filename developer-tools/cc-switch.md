# CC Switch

- **地址**：https://github.com/farion1231/cc-switch
- **作者**：Jason Young
- **协议**：MIT
- **分类**：开发者工具

## 简介

一个跨平台桌面应用，统一管理 Claude Code、Codex、Gemini CLI、OpenCode 和 OpenClaw 五种 AI 编程 CLI 工具。通过可视化界面一键切换 API Provider，无需手动编辑配置文件。内置 50+ Provider 预设，支持 MCP/Prompts/Skills 统一管理。

## 核心能力

- **五合一管理**：Claude Code、Codex、Gemini CLI、OpenCode、OpenClaw 统一管理
- **50+ Provider 预设**：AWS Bedrock、NVIDIA NIM、各社区中转服务，复制 Key 即可导入
- **系统托盘快速切换**：无需打开主界面，托盘菜单直接切换 Provider
- **统一 MCP 面板**：跨四个应用管理 MCP Server，双向同步
- **Prompts 管理**：Markdown 编辑器，跨应用同步 CLAUDE.md / AGENTS.md / GEMINI.md
- **Skills 一键安装**：从 GitHub 仓库或 ZIP 安装，支持自定义仓库管理
- **本地代理 & 故障转移**：格式转换、自动故障转移、熔断器、请求修正
- **用量 & 费用追踪**：消费、请求数、Token 趋势图，自定义模型定价
- **会话管理器**：浏览、搜索、恢复所有应用的对话历史
- **云同步**：Dropbox、OneDrive、iCloud、WebDAV 跨设备同步

## 技术栈

| 层 | 技术 |
|----|------|
| 前端 | React 18 + TypeScript + Vite + TailwindCSS + shadcn/ui |
| 后端 | Tauri 2.8 + Rust + SQLite |
| 测试 | vitest + MSW + @testing-library/react |

## 安装

```bash
# macOS（推荐）
brew tap farion1231/ccswitch
brew install --cask cc-switch

# Arch Linux
paru -S cc-switch-bin

# Windows / 其他 Linux
# 从 GitHub Releases 下载安装包
```

支持 Windows 10+、macOS 12+、Ubuntu 22.04+。macOS 版已通过 Apple 代码签名和公证。

## 架构设计

- **SSOT**：所有数据存储在 `~/.cc-switch/cc-switch.db`（SQLite）
- **原子写入**：临时文件 + 重命名模式防止配置损坏
- **双层存储**：SQLite 存可同步数据，JSON 存设备级设置
- **双向同步**：切换时写入实时文件，编辑活跃 Provider 时从实时文件回填

## 亮点 / 个人评价

解决了 AI 编程工具生态碎片化的问题——五个 CLI 工具各有各的配置格式，手动切换容易出错。CC Switch 用一个桌面 App 把它们统一管起来，50+ 预设覆盖了主流 Provider。本地代理 + 故障转移对依赖第三方中转服务的用户尤其实用。Tauri 2 + Rust 的架构保证了轻量和性能。对同时使用多个 AI 编程工具的开发者来说是必备工具。
