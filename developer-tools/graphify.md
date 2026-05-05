# Graphify

- **地址**：https://github.com/safishamsi/graphify
- **官网**：https://graphifylabs.ai
- **作者**：Safi Shamsi
- **分类**：开发者工具

## 简介

一个 AI 编程助手技能（Skill），在 Claude Code、Codex、Cursor、Gemini CLI 等 16+ 个 AI 编程工具中输入 `/graphify` 即可运行。它读取项目文件，构建知识图谱，帮助开发者快速理解代码库结构、发现架构决策背后的原因。支持代码、PDF、Markdown、截图、图表、白板照片、视频音频等多模态输入，从中提取概念和关系并连接成统一图谱。

## 核心特性

- **三阶段提取**：AST 确定性提取（代码结构）→ 本地 Whisper 转录（音视频）→ LLM 语义提取（文档/图片/转录）
- **25 语言 AST 支持**：通过 tree-sitter 解析 Python、JS/TS、Go、Rust、Java、C/C++、Ruby、C#、Kotlin 等 25 种编程语言
- **全模态输入**：代码、文档、PDF 论文、图片、视频、音频、YouTube URL，甚至 Office 文档
- **Leiden 社区检测**：基于图拓扑的聚类，无需嵌入或向量数据库
- **置信度标注**：每条关系标记为 `EXTRACTED`（源码中找到）、`INFERRED`（合理推断+置信度分数）或 `AMBIGUOUS`（需审查）
- **Token 节省**：查询时比读取原始文件减少 71.5x token 消耗（52 文件混合语料实测）
- **增量更新**：SHA256 缓存机制，重新运行只处理变更文件
- **MCP 服务器**：可暴露 `graph.json` 为 MCP 服务，支持结构化图查询

## 输出产物

```
graphify-out/
├── graph.html       # 交互式图谱（浏览器打开，点击节点、搜索、按社区过滤）
├── GRAPH_REPORT.md  # 核心节点、意外连接、建议问题
├── graph.json       # 持久化图谱（可跨会话查询）
└── cache/           # SHA256 缓存（仅处理变更文件）
```

## 支持平台（16+）

| 平台 | 集成方式 |
|------|----------|
| Claude Code | CLAUDE.md + PreToolUse Hook |
| Codex | AGENTS.md + PreToolUse Hook |
| Cursor | `.cursor/rules/graphify.mdc` |
| Gemini CLI | GEMINI.md + BeforeTool Hook |
| VS Code Copilot Chat | `.github/copilot-instructions.md` |
| GitHub Copilot CLI | Skill 文件 |
| Aider / OpenClaw / Trae / Kiro | AGENTS.md |
| Google Antigravity | `.agents/rules/` + `.agents/workflows/` |

## 安装与使用

```bash
# 安装
uv tool install graphifyy && graphify install
# 或
pip install graphifyy && graphify install

# PyPI 包名为 graphifyy（双 y），CLI 命令为 graphify
```

```bash
/graphify .                        # 当前目录构建图谱
/graphify ./raw --mode deep        # 深度模式，更积极的推断提取
/graphify ./raw --update           # 增量更新，仅处理变更文件
/graphify ./raw --watch            # 自动同步，文件变更时更新图谱

/graphify add https://arxiv.org/abs/1706.03762   # 添加论文
/graphify add <video-url>                         # 添加视频

/graphify query "show the auth flow"              # 查询图谱
/graphify path "DigestAuth" "Response"            # 最短路径
/graphify explain "SwinTransformer"               # 解释节点

graphify claude install            # 让 Claude 始终使用图谱
graphify hook install              # Git 钩子，提交/切换分支时自动重建
```

## 技术栈

NetworkX + Leiden (graspologic) + tree-sitter + vis.js + faster-whisper + yt-dlp

## 亮点 / 个人评价

- **填补了 AI 编程助手的认知空白**：传统 AI 编程工具通过 Grep/Glob 搜索文件，graphify 让 AI 先读图谱理解全局结构，再精准定位，大幅提升理解效率
- **跨平台通用性极强**：16+ 个 AI 编程工具一键集成，是目前覆盖最广的 AI 编程 Skill
- **多模态统一图谱**：将代码、论文、截图、视频、音频全部纳入同一知识图谱，非常适合研究型项目
- **隐私友好**：代码通过 tree-sitter 本地处理不外传，音视频通过本地 Whisper 转录不上传，只有文档/图片需要 LLM API
- **团队协作友好**：`graphify-out/` 设计为可提交 git，团队成员拉取即用
- **Karpathy 风格**：解决的是 Andrej Karpathy 提出的 `/raw` 文件夹问题——如何高效管理散落的论文、笔记、截图
