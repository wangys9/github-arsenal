# Professor Synapse

- **地址**：https://github.com/ProfSynapse/Professor-Synapse
- **作者/团队**：ProfSynapse
- **分类**：AI Agent

## 简介

Professor Synapse 是一个 AI Agent 编排提示词/技能，扮演"智慧导师"角色，根据用户任务自动召唤（Summon）匹配的专家 Agent 来解决问题。它不是传统意义上的代码框架，而是一套精心设计的 Prompt 工程体系，可运行在 ChatGPT、Claude、Gemini 等任意 LLM 上。

## 核心特性

- **专家 Agent 召唤**：根据任务需求，使用结构化模板动态创建专属专家 Agent
- **上下文收集**：通过针对性提问理解用户目标和偏好，再匹配合适的 Agent
- **自建 Agent 库**（Claude Skill 模式）：创建的 Agent 会自动保存，后续会话可复用
- **模式学习**：记录有效的交互模式和反模式，持续优化 Agent 质量
- **Multi-Agent 辩论**（Convener Protocol）：复杂决策时召集多个专家 Agent 进行结构化辩论，综合不同视角给出建议
- **智能更新**：从 GitHub 拉取更新时保留用户自定义的 Agent 和学习记录

## 两种使用方式

### 1. Universal Prompt（通用模式）

复制 `Prompt.md` 内容到任意 AI 的系统提示词即可使用，适用于 ChatGPT、Claude、Gemini 等所有 LLM。

### 2. Claude Skill（自建模式）

更强大的版本，作为 Claude Skill 安装，具备：

- Domain Researcher Agent（创建新专家前先联网研究领域）
- 自动索引和注册 Agent
- 交互模式学习与持久化
- GitHub 更新合并

## Skill 结构

```
professor-synapse/
├── SKILL.md                    # 主身份 + 工作流
├── agents/
│   ├── INDEX.md                # 自动生成的 Agent 注册表
│   └── domain-researcher.md    # 领域研究基础 Agent
├── references/
│   ├── learned-patterns.md     # 有效模式 + 反模式记录
│   ├── agent-template.md       # 新 Agent 结构模板
│   ├── convener-protocol.md    # 多 Agent 辩论协议
│   └── update-protocol.md      # 更新协议
└── scripts/
    └── rebuild-index.sh        # 重建索引脚本
```

## 交互流程

1. 用户提出需求 → Professor Synapse 问候并收集上下文
2. 评估复杂度 → 决定单个 Agent 或多 Agent 辩论
3. 单 Agent 路径：查找已有匹配 Agent，或召唤 Domain Researcher 研究后创建新 Agent
4. 多 Agent 路径（Convener）：召集多个专家进行结构化辩论，综合建议
5. 保存新 Agent → 更新模式学习记录

## 亮点 / 个人评价

这个项目代表了 Prompt 工程的一种高级范式——不写代码，纯靠精心设计的提示词实现 Agent 编排、记忆持久化和多 Agent 协作。适合想要深入理解 Prompt Engineering 和 Agent 设计模式的开发者学习参考。Claude Skill 版本展示了如何利用 Claude 的 Skill 机制构建可进化的 Agent 系统。
