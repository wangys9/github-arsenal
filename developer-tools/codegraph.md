# CodeGraph

- **地址**：https://github.com/colbymchenry/codegraph
- **作者/团队**：Colby McHenry
- **协议**：MIT
- **分类**：开发者工具

## 简介

CodeGraph 是一个本地代码知识图谱索引工具，通过 MCP 协议为 Claude Code、Cursor、Codex CLI、Gemini CLI、OpenCode、Hermes Agent、Antigravity IDE、Kiro 等 AI 编程 Agent 提供语义级代码理解能力。它将代码库预索引为符号关系图（函数、类、调用链、引用），Agent 查询图谱即可获得上下文，无需反复 grep/Read 扫描文件，显著降低 Token 消耗和工具调用次数。

## 核心特性

- **预索引知识图谱**：基于 tree-sitter 解析源码，提取符号节点和关系边（调用、导入、继承），存储到本地 SQLite（FTS5 全文搜索）
- **10 个 MCP 工具**：`codegraph_search`、`codegraph_context`、`codegraph_trace`、`codegraph_explore`、`codegraph_callers`、`codegraph_callees`、`codegraph_impact`、`codegraph_node`、`codegraph_files`、`codegraph_status`
- **调用路径追踪**：`codegraph_trace` 追踪两个符号间的完整调用链，支持动态分派跳转（回调、React 重渲染、接口→实现）
- **批量代码探索**：`codegraph_explore` 一次调用返回多个相关符号的源码，按文件分组并附带关系图
- **实时自动同步**：监听文件系统事件（FSEvents/inotify/ReadDirectoryChangesW），2 秒防抖增量更新；变更期间的查询会标记过期文件提醒 Agent 直接 Read
- **23+ 语言支持**：TypeScript、JavaScript、Python、Go、Rust、Java、C#、PHP、Ruby、C/C++、Objective-C、Swift、Kotlin、Scala、Dart、Svelte、Vue、Liquid、Pascal/Delphi、Lua、Luau 等
- **框架路由识别**：自动识别 14 个 Web 框架的路由定义（Django、Flask、FastAPI、Express、NestJS、Laravel、Drupal、Rails、Spring、Gin/chi、Axum/actix/Rocket、ASP.NET、Vapor、React Router/SvelteKit）
- **跨语言桥接**：Swift ↔ ObjC 自动桥接、React Native Legacy Bridge + TurboModules + Fabric 视图组件、Expo Modules、native → JS 事件发射器
- **影响分析**：`codegraph affected` 追踪变更文件的传递依赖，找出受影响的测试文件，适合 CI 集成
- **100% 本地运行**：无外部 API 调用，无数据外泄，所有数据存于 `.codegraph/codegraph.db`

## 性能基准（v0.9.4，2026-05-24 重新验证）

在 7 个真实开源项目上测试（Claude Opus 4.7 headless 模式，每个项目 4 次取中位数）：

| 项目 | 语言/规模 | 成本 | Token | 时间 | 工具调用 |
|------|----------|------|-------|------|---------|
| VS Code | TS · ~10k 文件 | 26% ↓ | 78% ↓ | 52% ↓ | 85% ↓ |
| Excalidraw | TS · ~640 文件 | 52% ↓ | 90% ↓ | 73% ↓ | 96% ↓ |
| Django | Python · ~3k | 12% ↓ | 36% ↓ | 19% ↓ | 53% ↓ |
| Tokio | Rust · ~790 | 82% ↓ | 86% ↓ | 71% ↓ | 92% ↓ |
| OkHttp | Java · ~645 | 2% ↓ | 13% ↓ | 31% ↓ | 45% ↓ |
| Gin | Go · ~110 | 21% ↓ | 34% ↓ | 27% ↓ | 40% ↓ |
| Alamofire | Swift · ~110 | 47% ↓ | 64% ↓ | 48% ↓ | 83% ↓ |

平均：**35% 更便宜、57% 更少 Token、46% 更快、71% 更少工具调用**

收益与代码库规模正相关：大型项目上 Agent 从索引直接回答、零文件读取；小型项目原生搜索已够便宜，差距收窄。

## 安装与使用

```bash
# 一键安装（自带 Node 运行时，无需预装 Node）
curl -fsSL https://raw.githubusercontent.com/colbymchenry/codegraph/main/install.sh | sh

# 或通过 npm
npx @colbymchenry/codegraph

# 初始化项目索引
cd your-project && codegraph init -i

# 搜索符号
codegraph query "UserService"

# 查找变更影响的测试文件（CI 集成）
git diff --name-only | codegraph affected --stdin
```

支持 8 种 Agent 自动配置：Claude Code、Cursor、Codex CLI、OpenCode、Hermes Agent、Gemini CLI、Antigravity IDE、Kiro。

也支持作为 Node.js 库使用：`import CodeGraph from '@colbymchenry/codegraph'`

## 工作原理

```
源码 → tree-sitter AST 解析 → 提取符号节点 + 关系边 → SQLite 图数据库
                                                          ↕
AI Agent ← MCP 协议查询 ← codegraph serve --mcp（文件监听自动同步）
```

1. **提取**：tree-sitter 解析源码为 AST，语言特定查询提取节点和边
2. **存储**：存入本地 SQLite（WAL 模式），FTS5 全文索引
3. **解析**：函数调用→定义、导入→源文件、类继承、框架路由模式、跨语言桥接
4. **同步**：MCP Server 监听文件变更 → 防抖增量更新 → 变更期间查询标记过期文件

## 亮点 / 个人评价

这是目前最成熟的 AI 编程 Agent 代码理解增强方案之一。核心思路清晰：预先建好索引直接查询，而非让 Agent 每次通过 grep/Read 探索代码库。v0.9.4 的基准数据在大型项目（VS Code ~10k 文件）上效果尤为显著——成本降低 26%、工具调用减少 85%。

跨语言桥接是独特亮点，能追踪 Swift↔ObjC、React Native↔Native 的完整调用链，这在静态分析工具中很少见。`codegraph trace` 支持动态分派跳转（回调和接口→实现），超越了普通 grep 的能力。零配置设计（自动排除 node_modules/dist、自动识别 .gitignore）和全平台自包含构建（内置 Node 运行时）也降低了使用门槛。
