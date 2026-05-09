---
name: github-archive
description: |
  通过 GitHub 项目地址，自动获取项目信息、生成中文总结，并按分类归档到
  /Users/july/workspace/Vault/idea/github/ 目录下。自动根据项目内容判断分类，
  创建对应分类文件夹，每个项目生成独立的 Markdown 文件。
  当用户提供 GitHub URL 并要求归档、总结、记录、收藏项目时触发。
  触发场景：用户粘贴 GitHub 链接并说"归档"、"总结"、"记录一下"、
  "收藏这个"、"archive"等，或在讨论 GitHub 项目后要求保存记录。
---

# GitHub 项目归档

将 GitHub 项目信息总结归档到本地知识库，按分类组织。

## 归档目录

```
/Users/july/workspace/Vault/idea/github/
├── README.md              # 分类索引（自动维护）
├── ai-agent/              # AI Agent 平台、框架、协作工具
│   └── project-name.md
├── ai-learning/           # AI/ML 学习资源、教程、课程
│   └── project-name.md
├── llm-tools/             # 大模型工具（训练、推理、微调、部署）
│   └── project-name.md
├── design-ui/             # 设计系统、UI 框架、前端工具
│   └── project-name.md
├── developer-tools/       # 开发者工具、IDE、CLI、编辑器
│   └── project-name.md
├── search-knowledge/      # 搜索引擎、知识管理、文档工具
│   └── project-name.md
├── devops-infra/          # DevOps、基础设施、云原生、数据库
│   └── project-name.md
├── data-analytics/        # 数据分析、可视化、BI 工具
│   └── project-name.md
├── security/              # 安全工具、安全研究、CTF
│   └── project-name.md
└── other/                 # 其他无法归类的项目
    └── project-name.md
```

以上是常见分类，如果项目不属于任何已有分类，可创建新的分类文件夹。分类名称使用小写英文、短横线分隔。

## 工作流程

### 第一步：获取项目信息

1. 从用户消息中提取 GitHub URL，解析出 owner/repo
2. 使用 GitHub MCP 工具获取 `README.md` 内容：
   - `get_file_contents(owner, repo, "README.md")`
3. 如果 README 内容不够丰富，可补充获取：
   - 仓库描述、语言、Star 数等（通过 `gh repo view`）
   - `CONTRIBUTING.md` 或 `docs/` 目录中的额外信息

### 第二步：分析并分类

根据项目内容判断分类，参考以下维度：

| 分类 | 判断依据 |
|------|----------|
| ai-agent | Agent 框架、多 Agent 协作、Agent 平台、自治系统 |
| ai-learning | 教程、课程、学习指南、编程实践、教材 |
| llm-tools | LLM 训练/推理/微调工具、模型部署、RAG、向量数据库 |
| design-ui | 设计系统、UI 组件库、CSS 框架、图标、排版 |
| developer-tools | IDE、CLI、编辑器插件、调试工具、代码生成 |
| search-knowledge | 搜索引擎、笔记工具、知识图谱、文档管理 |
| devops-infra | CI/CD、容器、K8s、数据库、监控、日志 |
| data-analytics | 数据可视化、BI、报表、统计分析、图表库 |
| security | 安全扫描、渗透测试、加密、认证、CTF |

如果项目横跨多个领域，选择最核心的一个。如果不在上述分类中，创建新分类文件夹。

### 第三步：生成总结

使用中文撰写项目总结，包含以下结构：

```markdown
# 项目名称

- **地址**：https://github.com/owner/repo
- **官网**：（如有）
- **作者/团队**：（如有知名作者）
- **协议**：（开源协议）
- **分类**：（所属分类）

## 简介

一段话概括项目是什么、解决什么问题。突出核心价值主张。

## 核心特性

- 特性 1：简要说明
- 特性 2：简要说明
- ...

（根据项目内容选择合适的组织方式，不必严格遵循固定模板）

## 技术栈 / 架构

（如果项目有明确的技术栈或架构设计，用表格或列表展示）

## 安装 / 使用

（简要的安装或使用方式，如有）

## 亮点 / 个人评价

（这个项目为什么值得关注，有什么独特之处）
```

**写作原则**：
- 全部使用中文
- 保持简洁，抓住重点，不要面面俱到地翻译 README
- 专注于"这是什么、为什么有用、怎么用"
- 技术术语保留英文原文（如 Agent、RAG、Fine-tuning）
- 代码示例仅保留最有代表性的片段

### 第四步：写入文件

1. **确定文件路径**：
   - 分类文件夹：`/Users/july/workspace/Vault/idea/github/{category}/`
   - 文件名：使用 repo 名称（小写，与 GitHub 一致），如 `dive-into-llms.md`

2. **创建文件夹**（如果不存在）

3. **写入项目文件**：
   - 将总结内容写入 `/Users/july/workspace/Vault/idea/github/{category}/{repo-name}.md`

### 第五步：更新索引

更新 `/Users/july/workspace/Vault/idea/github/README.md`，维护分类索引：

```markdown
# GitHub 项目归档

> 按分类整理的 GitHub 开源项目收藏

## 分类索引

### AI Agent
- [Multica — AI Agent 托管协作平台](ai-agent/multica.md)

### 搜索与知识管理
- [QMD — 本地文档搜索引擎](search-knowledge/qmd.md)

### ...
```

每个分类下列出所有已归档的项目，格式：`- [项目名 — 一句话描述](分类路径/文件名.md)`

## 处理现有归档文件

如果已存在旧的合并文件 `ai-agent-projects.md`（所有项目在一个文件中），不要删除它。新归档的项目按新结构存放，旧文件保留原样。

## 批量归档

如果用户一次提供多个 GitHub URL，逐个处理，全部完成后统一更新索引文件。
