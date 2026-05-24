# CodeWiki

- **地址**：https://github.com/FSoft-AI4Code/CodeWiki
- **作者/团队**：FSoft-AI4Code（FPT Software AI4Code 团队）
- **协议**：MIT
- **论文**：ACL 2026（arXiv:2510.24428）
- **分类**：开发者工具

## 简介

CodeWiki 是一个 AI 驱动的代码库文档自动生成框架，能为大型代码仓库生成整体性的、结构化的文档。不同于只生成函数级注释的工具，CodeWiki 关注跨文件、跨模块、系统级的交互关系，输出包含架构图、数据流图、序列图在内的多模态文档。支持 8 种编程语言，已在 86K-1.4M LOC 的项目上验证。

## 核心特性

- **层级分解（Hierarchical Decomposition）**：受动态规划启发，将代码库递归分解为内聚模块，保持架构上下文不丢失
- **递归多 Agent 处理**：自适应多 Agent 协作，支持动态任务委派，可处理任意规模的代码库
- **多模态合成**：同时生成文本文档和可视化产物（Mermaid 架构图、数据流图、依赖关系图、序列图）
- **增量更新**：`--update` 模式仅重新生成自上次运行以来变更的模块
- **GitHub Pages 集成**：`--github-pages` 一键生成可浏览的 HTML 文档站
- **多 LLM 后端**：支持 OpenAI、Anthropic、AWS Bedrock、Azure OpenAI

## 支持 8 种语言

Python、Java、JavaScript、TypeScript、C、C++、C#、Kotlin

## 基准测试（CodeWikiBench）

在 21 个仓库上与 DeepWiki 对比：

| 语言类别 | CodeWiki | DeepWiki | 提升 |
|----------|----------|----------|------|
| 高级语言（Python/JS/TS） | 79.14% | 68.67% | +10.47% |
| 托管语言（C#/Java） | 68.84% | 64.80% | +4.04% |
| 系统语言（C/C++） | 53.24% | 56.39% | -3.15% |
| **总体** | **68.79%** | **64.06%** | **+4.73%** |

## 工作原理

三阶段流水线：

```
代码库 → 层级分解 → 递归多 Agent 处理 → 多模态合成 → 文档输出
                                                    → 可视化图表（Mermaid）
```

1. **层级分解**：将仓库拆分为内聚模块，保留架构上下文
2. **多 Agent 处理**：Agent 自适应处理各模块，复杂模块自动委派子 Agent
3. **多模态合成**：整合文本描述与可视化图表

## 安装与使用

```bash
# 安装
pip install git+https://github.com/FSoft-AI4Code/CodeWiki.git

# 配置 LLM
codewiki config set --api-key YOUR_KEY --base-url https://api.anthropic.com --main-model claude-sonnet-4

# 生成文档
cd /path/to/project
codewiki generate

# 生成 HTML 文档站并创建 Git 分支
codewiki generate --github-pages --create-branch

# 增量更新（只重新生成变更模块）
codewiki generate --update
```

输出结构：

```
./docs/
├── overview.md              # 仓库概览（入口）
├── module1.md               # 模块文档
├── module_tree.json         # 层级模块结构
├── metadata.json            # 生成元数据
└── index.html               # 交互式文档查看器
```

## 亮点 / 个人评价

这是目前最完整的 AI 代码库文档生成方案之一。核心创新在于"层级分解 + 递归 Agent"的组合——不是简单地把所有代码塞给 LLM，而是先分解为模块再逐层处理，这使得它能在百万行级别的项目上工作。ACL 2026 论文背书，学术严谨性和工程质量兼备。`--update` 增量模式和 `--github-pages` 一键部署是实用加分项。唯一的短板是 C/C++ 项目上表现略逊于 DeepWiki。
