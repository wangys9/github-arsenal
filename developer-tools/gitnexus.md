# GitNexus

- **地址**：https://github.com/abhigyanpatwari/GitNexus
- **官网**：https://gitnexus.vercel.app
- **作者**：abhigyanpatwari（Akon Labs）
- **协议**：PolyForm Noncommercial（非商业使用免费，商业需授权）
- **分类**：开发者工具

## 简介

零服务器的代码智能引擎。将任意代码库索引为知识图谱——追踪每个依赖、调用链、功能集群和执行流——通过 MCP 工具暴露给 AI Agent，让 Cursor、Claude Code、Codex 等 AI 编程工具真正理解代码架构，避免遗漏依赖、破坏调用链。

核心定位：`harness + model = agent`。传统 Graph RAG 让 LLM 自己探索图谱，GitNexus 在索引阶段就预计算好聚类、流程追踪、置信度评分，工具一次调用即可返回完整上下文。

## 核心特性

- **知识图谱索引**：多阶段管道——文件结构 → AST 解析 → 导入/调用解析 → 聚类 → 执行流追踪 → 混合搜索索引
- **16 个 MCP 工具**：查询、上下文分析、影响范围分析、变更检测、多文件重命名、Cypher 查询、多仓库组管理等
- **14 种语言支持**：TypeScript、JavaScript、Python、Java、Kotlin、C#、Go、Rust、PHP、Ruby、Swift、C、C++、Dart
- **双使用方式**：CLI + MCP（本地索引，连接 AI Agent）和 Web UI（浏览器可视化图谱 + AI 对话）
- **多仓库支持**：全局注册表机制，一个 MCP 服务器服务多个已索引仓库
- **Wiki 生成**：从知识图谱自动生成 LLM 驱动的代码文档
- **Agent Skills**：自动安装探索、调试、影响分析、重构四个 Agent 技能到 `.claude/skills/`
- **数据完全本地**：CLI 模式下无网络调用，Web 模式下一切在浏览器运行

## 传统 Graph RAG vs GitNexus

| 维度 | 传统 Graph RAG | GitNexus |
|------|----------------|----------|
| 查询方式 | LLM 多轮探索图谱 | 预计算结构，一次调用返回完整上下文 |
| 可靠性 | LLM 可能遗漏上下文 | 工具响应已包含完整信息 |
| Token 效率 | 10+ 查询链理解一个函数 | 1 次查询获取全部上下文 |
| 模型门槛 | 需要强模型探索 | 小模型也能工作，工具做重活 |

## 技术栈

| 层 | CLI | Web |
|---|-----|-----|
| 运行时 | Node.js（原生） | 浏览器（WASM） |
| 解析 | Tree-sitter 原生绑定 | Tree-sitter WASM |
| 数据库 | LadybugDB 原生 | LadybugDB WASM |
| 向量 | transformers.js（GPU/CPU） | transformers.js（WebGPU/WASM） |
| 搜索 | BM25 + 语义 + RRF | BM25 + 语义 + RRF |
| 可视化 | — | Sigma.js + Graphology（WebGL） |
| 前端 | — | React 18 + TypeScript + Vite + Tailwind v4 |

## 编辑器支持

| 编辑器 | MCP | Skills | Hooks | 支持 |
|--------|-----|--------|-------|------|
| Claude Code | 是 | 是 | PreToolUse + PostToolUse | 完整 |
| Cursor | 是 | 是 | PostToolUse | 完整 |
| Codex | 是 | 是 | — | MCP + Skills |
| Windsurf | 是 | — | — | MCP |
| OpenCode | 是 | 是 | — | MCP + Skills |

## 安装与使用

```bash
# 一键索引（从仓库根目录运行）
npx gitnexus analyze

# 配置 MCP（一次性）
npx gitnexus setup

# 启动本地 HTTP 服务（Web UI 连接）
npx gitnexus serve

# Claude Code 手动配置
claude mcp add gitnexus -- npx -y gitnexus@latest mcp
```

`analyze` 命令会自动完成：索引代码库、安装 Agent Skills、注册 Claude Code Hooks、生成 `AGENTS.md` / `CLAUDE.md` 上下文文件。

## 亮点 / 个人评价

GitNexus 解决了 AI 编程工具最核心的问题——它们不知道代码库的结构。通过预计算的知识图谱，即使是小模型也能获得完整的架构视图，做出更可靠的编辑决策。39.4k Star 说明社区认可度极高。Claude Code 的深度集成（MCP + Skills + Hooks）让它在 AI 编程工作流中几乎是即插即用的。注意协议是 PolyForm Noncommercial，商业使用需要联系 Aka Labs 获取授权。
