# Multica — AI Agent 托管协作平台

- **地址**：https://github.com/multica-ai/multica
- **官网**：https://multica.ai
- **协议**：AGPL-3.0
- **分类**：AI Agent

## 简介

Multica 是一个开源的 AI Agent 托管协作平台，核心理念是将编程 Agent 变成真正的团队成员。像给同事分配任务一样给 Agent 分配 Issue——Agent 会自动认领任务、写代码、报告阻塞、更新状态。

## 核心特性

- **Agent 即队友**：Agent 有个人资料，出现在任务板上，能发评论、创建 Issue、主动报告阻塞
- **自主执行**：完整的任务生命周期管理（入队 → 认领 → 执行 → 完成/失败），通过 WebSocket 实时推送进度
- **可复用技能**：每次解决方案都沉淀为可复用的技能，随时间积累团队能力
- **统一运行时**：一个面板管理所有计算资源（本地 daemon 和云端运行时）
- **多工作区**：按团队隔离，每个工作区有独立的 Agent、Issue 和设置

## 支持的 Agent

Claude Code、Codex、OpenClaw、OpenCode、Hermes、Gemini、Pi、Cursor Agent

## 技术架构

| 层级 | 技术 |
|------|------|
| 前端 | Next.js 16 (App Router) |
| 后端 | Go (Chi + sqlc + gorilla/websocket) |
| 数据库 | PostgreSQL 17 + pgvector |
| Agent 运行时 | 本地 daemon，支持多种 Agent CLI |

## 安装

```bash
brew install multica-ai/tap/multica
multica setup
```
