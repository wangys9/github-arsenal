# awesome-agentic-ai-zh

- **地址**：https://github.com/WenyuChiou/awesome-agentic-ai-zh
- **作者**：[@WenyuChiou](https://github.com/WenyuChiou)
- **协议**：MIT
- **语言**：繁体中文（主）/ 简体中文 / English
- **分类**：AI 学习资源

## 简介

一份结构化的 AI Agent 学习路线图，从"LLM 是什么"一路带你走到"自己打造多 Agent 系统"。将散落网络的高质量项目、教材、动手练习按 7 个阶段组织，每阶段明确指出**该学什么、必做哪些练习、推荐哪些项目、进阶前的检查点**。

## 核心特性

- **两条学习路径**：Track A（CLI Power User）面向想用现成 CLI Agent 的人；Track B（Agent Builder）面向想从零构建 Agent 的人。Stage 0-2 为共用基础
- **7 阶段渐进式学习**：从 Python/API 基础 → LLM 入门 → Prompt 设计 → Tool Use & Agent → Agent 框架 → Claude Code 生态 → Memory/RAG → Multi-Agent
- **145+ 精选项目**：每个项目附带星等推荐、适合人群、教学内容、运行方式
- **必做动手练习**：每阶段 1-5 个 mini project，强调"不动手学不会"
- **5 条按角色分流的延伸路线**：研究员 / 开发者 / 教师 / 知识工作者 / 日常使用者
- **完整 Claude Code 生态覆盖**：MCP / Skills / Plugins / SDK / Marketplace
- **配套资源**：术语表（30+ 词条）、Cookbook（6 个 step-by-step recipe）、MCP/Skills 目录（62 条）

## 学习路径概览

### 共用基础（Stage 0-2，约 3-5 周）

| Stage | 主题 | 内容 | 时程 |
|-------|------|------|------|
| 0 | 基础准备 | Python / CLI / git / API / JSON | 1-2 周 |
| 1 | LLM 入门 | Token / API / 各家 LLM 比较 / 本地 LLM | 1 周 |
| 2 | Prompt 设计 | 系统 Prompt / Few-shot / CoT | 1-2 周 |

### Track A — CLI Power User（约 3-5 周）

| Stage | 主题 | 内容 |
|-------|------|------|
| A1 | CLI Agent 入门 | 6 主流 CLI 比较 / 安装 / 首次运行 |
| A2 | CLI Workflow | CLAUDE.md / Slash Command / 多步骤拆解 |
| A3 | 集成与生产化 | MCP 接 CLI / CI 自动化 / 成本与可观测性 |

### Track B — Agent Builder（约 14-19 周）

| Stage | 主题 | 内容 |
|-------|------|------|
| 3 | Tool Use & Agent | Function Calling / ReAct / 5 个动手练习 |
| 4 | Agent 框架 | LangGraph / AutoGen / CrewAI / Smolagents |
| 5 | Claude Code 生态 | MCP / Skills / Plugins / Marketplace |
| 6 | Memory & RAG | 向量数据库 / 长期记忆 / Contextual Retrieval |
| 7 | Multi-Agent 进阶 | 多 Agent 编排 / 评估 / 可观测性 / SDK |

## 亮点 / 个人评价

- **路径设计非常用心**：不是简单的资源堆砌，而是有明确的学习顺序和每阶段的检查点，适合按部就班地系统学习
- **Track A/B 分流**很实用：不一定要成为 Agent 开发者，只想用好 CLI 工具的人也有清晰路径
- **中文友好**：繁体中文为主，对中文学习者非常友好
- **配套完善**：术语表、Cookbook、MCP 目录等辅助资源齐全，不只是路线图本身
- **与现实接轨**：预估时程写得很诚实（5-6 个月兼职），且有按角色分流的延伸路线
