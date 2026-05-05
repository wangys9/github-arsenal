# Code Review Graph

- **地址**：https://github.com/tirth8205/code-review-graph
- **官网**：https://code-review-graph.com
- **协议**：MIT
- **分类**：开发者工具

## 简介

一个本地代码知识图谱工具，用 Tree-sitter 将代码库解析为函数、类、调用关系组成的图结构，通过 MCP 协议提供给 AI 编程助手精确上下文，避免 AI 每次任务都重新阅读整个代码库。实测在 6 个真实项目上平均减少 8.2x Token 消耗，Monorepo 场景下可达 49x。

## 核心特性

- **Blast-radius 分析**：文件变更时，追踪所有调用方、依赖方和测试，AI 只读取受影响的文件
- **增量更新 < 2 秒**：基于 SHA-256 哈希检测变更，只重新解析修改的文件（2900 文件项目 < 2 秒）
- **28 个 MCP 工具**：构建、查询、遍历、搜索、变更检测、架构概览、知识缺口分析等
- **23 种语言 + Jupyter**：Python、TS/JS、Go、Rust、Java、C#、Ruby、Kotlin、Swift、PHP、C/C++ 等
- **语义搜索**：可选向量嵌入（sentence-transformers、Google Gemini、OpenAI 兼容端点）
- **多仓库支持**：注册多个仓库，跨仓库搜索，后台守护进程自动更新
- **11 个 AI 平台**：自动检测并配置 Claude Code、Cursor、Codex、Windsurf、Zed、Continue 等

## 工作流程

```
代码库 → Tree-sitter 解析 → SQLite 图存储
                                    ↓
         MCP 查询 ← Blast-radius 分析 ← 变更检测
                    ↓
            AI 只读取受影响的文件
```

## 性能基准

| 项目 | 文件数 | 节点 | 边 | Token 削减 |
|------|--------|------|-----|-----------|
| Next.js | — | — | — | 8.0x |
| Gin | 99 | 1,286 | 16,762 | 16.4x |
| Flask | 83 | 1,446 | 7,974 | 9.1x |
| FastAPI | 1,122 | 6,285 | 27,117 | 8.1x |
| HTTPX | 60 | 1,253 | 7,896 | 6.9x |

影响分析准确率：100% 召回率（不漏报），平均 F1 = 0.54。

## 安装使用

```bash
pip install code-review-graph
code-review-graph install    # 自动检测 AI 平台并配置 MCP
code-review-graph build      # 解析代码库
```

安装后重启编辑器，AI 助手会自动通过 MCP 使用图谱工具。

## 主要 CLI 命令

```bash
code-review-graph build              # 构建图
code-review-graph update             # 增量更新
code-review-graph watch              # 监听文件变化自动更新
code-review-graph visualize          # 生成 D3.js 交互式可视化
code-review-graph detect-changes     # 变更影响分析
code-review-graph wiki               # 从社区结构生成 Wiki
code-review-graph daemon start       # 启动多仓库守护进程
```

## 技术架构

- **存储**：SQLite 本地文件（`.code-review-graph/`），无外部数据库依赖
- **解析**：Tree-sitter AST 解析，支持函数/类/导入/调用/继承关系
- **社区检测**：Leiden 算法聚类，超大社区自动拆分
- **搜索**：FTS5 全文搜索 + 可选向量语义搜索
- **导出**：GraphML（Gephi）、Neo4j Cypher、Obsidian Vault、SVG

## 亮点 / 个人评价

解决了 AI 编程工具的核心痛点——每次任务都重读整个代码库浪费 Token。Blast-radius 分析让 AI 只关注变更影响范围，效果立竿见影。28 个 MCP 工具覆盖了从代码审查、架构分析到知识缺口检测的完整场景。增量更新 < 2 秒保证了日常使用的流畅性。多平台自动检测安装降低了配置门槛。对使用 Claude Code / Cursor 等 AI 编程工具的开发者来说，这是显著提升效率和节省 Token 消耗的必备工具。
