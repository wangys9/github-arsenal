# CodeGraph

- **地址**：https://github.com/colbymchenry/codegraph
- **作者/团队**：Colby McHenry
- **协议**：MIT
- **分类**：开发者工具

## 简介

CodeGraph 是一个本地代码知识图谱索引工具，通过 MCP 协议为 Claude Code、Cursor、Codex CLI、OpenCode 等 AI 编程 Agent 提供语义级代码理解能力。它将代码库预索引为符号关系图（函数、类、调用链、引用），Agent 查询图谱即可获得上下文，无需反复 grep/Read 扫描文件，显著降低 Token 消耗和工具调用次数。

## 核心特性

- **预索引知识图谱**：基于 tree-sitter 解析源码，提取符号节点和关系边（调用、导入、继承），存储到本地 SQLite（FTS5 全文搜索）
- **8 个 MCP 工具**：`codegraph_search`、`codegraph_context`、`codegraph_callers`、`codegraph_callees`、`codegraph_impact`、`codegraph_node`、`codegraph_files`、`codegraph_status`
- **实时自动同步**：监听文件系统事件（FSEvents/inotify/ReadDirectoryChangesW），2 秒防抖增量更新，无需手动重建索引
- **19+ 语言支持**：TypeScript、JavaScript、Python、Go、Rust、Java、C#、PHP、Ruby、C/C++、Swift、Kotlin、Dart、Svelte、Vue、Liquid、Pascal/Delphi 等
- **框架路由识别**：自动识别 Django、Flask、FastAPI、Express、NestJS、Laravel、Rails、Spring、Gin 等 13 个框架的路由定义，将 URL 模式关联到处理函数
- **影响分析**：`codegraph affected` 命令可追踪变更文件的传递依赖，找出受影响的测试文件，适合 CI 集成
- **100% 本地运行**：无外部 API 调用，无数据外泄，所有数据存于 `.codegraph/codegraph.db`

## 性能基准

在 7 个真实开源项目上测试（Claude Opus 4.7 headless 模式，每个项目 4 次取中位数）：

| 项目 | 语言 | 成本节省 | Token 节省 | 速度提升 | 工具调用减少 |
|------|------|----------|-----------|---------|-------------|
| VS Code | TypeScript | 35% | 73% | 41% | 72% |
| Django | Python | 34% | 64% | 59% | 81% |
| Tokio | Rust | 52% | 81% | 63% | 89% |
| Excalidraw | TypeScript | 47% | 73% | 60% | 86% |

平均：**35% 更便宜、59% 更少 Token、49% 更快、70% 更少工具调用**

## 安装与使用

```bash
# 一键安装（交互式，自动检测已安装的 Agent）
npx @colbymchenry/codegraph

# 初始化项目索引
cd your-project
codegraph init -i

# 搜索符号
codegraph query "UserService"

# 查找变更影响的测试文件（CI 集成）
git diff --name-only | codegraph affected --stdin
```

支持 Claude Code、Cursor、Codex CLI、OpenCode 四种 Agent 自动配置。

## 工作原理

```
源码 → tree-sitter AST 解析 → 提取符号节点 + 关系边 → SQLite 图数据库
                                                          ↕
AI Agent ← MCP 协议查询 ← codegraph serve --mcp（文件监听自动同步）
```

1. **提取**：tree-sitter 解析源码为 AST，语言特定查询提取节点和边
2. **存储**：存入本地 SQLite，FTS5 全文索引
3. **解析**：函数调用→定义、导入→源文件、类继承、框架路由模式
4. **同步**：MCP Server 监听文件变更，防抖增量更新

## 亮点 / 个人评价

这是目前最成熟的 AI 编程 Agent 代码理解增强方案之一。核心思路很清晰：与其让 Agent 每次都通过 grep/Read 探索代码库，不如预先建好索引直接查询。35% 的成本节省和 70% 的工具调用减少是实打实的数字。特别适合大型代码库场景——小型项目（如 Gin ~150 文件）收益有限，但在万级文件的项目上效果显著。`codegraph affected` 命令追踪变更影响的测试文件也是一个很实用的 CI 集成点。
