# agent-skills

- **地址**：https://github.com/addyosmani/agent-skills
- **作者**：[@addyosmani](https://github.com/addyosmani)（Google 工程师，JavaScript 社区知名人物）
- **协议**：MIT
- **分类**：开发者工具

## 简介

一套生产级 AI 编程 Agent 工程技能包。将资深工程师在软件开发全生命周期中使用的工作流、质量门禁和最佳实践编码为结构化的 Skill，让 AI Agent 在每个阶段都遵循一致的高标准。

## 核心特性

- **7 个 Slash 命令**覆盖开发全流程：`/spec` → `/plan` → `/build` → `/test` → `/review` → `/code-simplify` → `/ship`
- **22 个结构化 Skill**：每个 Skill 都有明确的步骤、验证门禁和"反合理化"表格（防止 Agent 找借口跳过关键步骤）
- **3 个专家 Persona**：Code Reviewer（高级工程师视角）、Test Engineer（QA 专家视角）、Security Auditor（安全审计视角）
- **4 份参考清单**：测试模式、安全检查、性能优化、无障碍访问
- **多平台支持**：Claude Code（Marketplace 安装）、Cursor、Gemini CLI、Windsurf、OpenCode、GitHub Copilot、Kiro IDE

## Skill 设计哲学

- **流程而非文档**：Skill 是 Agent 遵循的工作流，不是参考读物
- **反合理化机制**：每个 Skill 都包含常见借口和反驳理由（如"我稍后补测试"）
- **验证不可妥协**：每个 Skill 都以证据要求结尾，"看起来对了"永远不够
- **渐进式加载**：`SKILL.md` 是入口，补充参考仅在需要时加载，节省 Token

## 技术来源

融入 Google 工程文化实践，包括：
- Hyrum's Law（API 设计）
- Beyonce Rule 和测试金字塔（测试）
- 变更大小和审查速度标准（代码审查）
- Chesterton's Fence（代码简化）
- 主干开发（Git 工作流）
- Shift Left 和功能开关（CI/CD）
- 代码即负债思维（废弃与迁移）

## 快速安装

```bash
# Claude Code Marketplace
/plugin marketplace add addyosmani/agent-skills
/plugin install agent-skills@addy-agent-skills

# Gemini CLI
gemini skills install https://github.com/addyosmani/agent-skills.git --path skills

# Cursor / 其他：复制 SKILL.md 到对应规则目录
```

## 亮点 / 个人评价

- **作者背书强**：Addy Osmani 是 Google Chrome 团队工程师，Learning Patterns、Image Optimization 等书的作者，工程实践可信度高
- **实战导向**：不是泛泛的 AI 提示，而是从 Google 工程实践中提炼的具体流程
- **"反合理化"设计很巧妙**：针对 AI Agent 常见的偷懒行为（跳过测试、跳过安全审查）设计了专门的应对机制
- **跨平台通用**：纯 Markdown 格式，理论上任何接受系统提示的 Agent 都能用
- **完整覆盖开发生命周期**：从需求定义到上线部署，每个环节都有对应的 Skill
