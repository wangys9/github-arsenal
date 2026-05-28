# Understand Anything

- **地址**：https://github.com/Lum1104/Understand-Anything
- **作者**：Lum1104
- **协议**：MIT
- **分类**：开发者工具

## 简介

将任意代码库转化为交互式知识图谱的 AI 插件工具。通过多 Agent 流水线分析项目，提取文件、函数、类、依赖关系，构建可视化知识图谱，支持探索、搜索和问答。兼容 Claude Code、Codex、Cursor、Copilot、Gemini CLI 等主流 AI 编码平台。

核心理念：**"能教会人的图谱 > 让人惊叹的图谱"** —— 不是展示代码有多复杂，而是让每个部分如何协同一目了然。

## 核心特性

- **结构图谱探索**：将代码库渲染为可交互的知识图谱，每个文件、函数、类都是可点击、可搜索的节点
- **业务领域视图**：切换到 Domain 视图，查看代码如何映射到真实业务流程（域、流、步骤）
- **知识库分析**：对 Karpathy 模式的 LLM Wiki 进行分析，提取实体、声明和隐含关系，生成可导航的知识图谱
- **引导式导览**：自动生成按依赖排序的架构导览，以正确顺序学习代码库
- **模糊与语义搜索**：按名称或语义搜索，如"哪些部分处理认证？"
- **Diff 影响分析**：提交前查看变更对系统的涟漪效应
- **Personna 自适应 UI**：根据角色（初级开发者、PM、高级用户）调整详情层级
- **分层可视化**：自动按架构层（API / Service / Data / UI / Utility）分组，色彩编码
- **增量更新**：默认只重新分析变更文件，支持 post-commit hook 自动更新

## 技术架构

### Tree-sitter + LLM 混合分析

| 层 | 职责 |
|---|---|
| **Tree-sitter（确定性）** | 解析源码为语法树，提取 imports/exports、函数/类定义、调用关系、继承关系。同输入 → 同输出，支持指纹变更检测 |
| **LLM（语义层）** | 基于解析结构 + 原始源码，生成自然语言摘要、标签、架构层分配、业务域映射、导览、编程概念标注 |

### 多 Agent 流水线

| Agent | 角色 |
|---|---|
| `project-scanner` | 发现文件、检测语言和框架 |
| `file-analyzer` | 提取函数/类/导入，生成图谱节点和边 |
| `architecture-analyzer` | 识别架构层 |
| `tour-builder` | 生成引导式学习导览 |
| `graph-reviewer` | 验证图谱完整性和引用完整性 |
| `domain-analyzer` | 提取业务域、流程和步骤 |
| `article-analyzer` | 从 Wiki 文章提取实体和关系 |

文件分析器并行运行（最多 5 并发，每批 20-30 个文件）。

## 安装与使用

### Claude Code

```bash
/plugin marketplace add Lum1104/Understand-Anything
/plugin install understand-anything
```

### 通用安装（Codex / Gemini CLI / Cursor / VS Code Copilot 等）

```bash
# macOS / Linux
curl -fsSL https://raw.githubusercontent.com/Lum1104/Understand-Anything/main/install.sh | bash

# Windows (PowerShell)
iwr -useb https://raw.githubusercontent.com/Lum1104/Understand-Anything/main/install.ps1 | iex
```

### 常用命令

```bash
/understand                    # 分析代码库，生成知识图谱
/understand --language zh      # 生成中文内容
/understand-chat 如何支付流程？  # 问答
/understand-diff               # 变更影响分析
/understand-explain src/auth   # 深入分析特定文件
/understand-onboard            # 生成新人上手指南
/understand-domain             # 提取业务领域知识
/understand --auto-update      # 每次 commit 自动更新图谱
```

### 团队协作

知识图谱就是 JSON 文件，可以提交到 Git 仓库。团队成员 clone 后直接使用，无需重新运行分析流水线。

## 亮点

- **跨平台兼容性极强**：15+ AI 编码平台支持，是目前覆盖面最广的 AI 编码插件之一
- **确定性 + 语义的混合方案**：Tree-sitter 保证结构可复现，LLM 提供深层语义理解，两者互补
- **增量更新设计**：大仓库不会每次全量扫描，只处理变更部分
- **图谱可提交**：作为 `docs-as-code` 的新形态，知识图谱随代码一起版本管理
- **多语言支持**：支持 en / zh / zh-TW / ja / ko / ru 等语言的输出内容
