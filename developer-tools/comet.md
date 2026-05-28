# Comet

- **地址**：https://github.com/rpamis/comet
- **作者/团队**：rpamis
- **协议**：MIT
- **分类**：developer-tools

## 简介

Comet 是一个将 OpenSpec 和 Superpowers 两个 Skill 项目融合的双星开发工作流工具。OpenSpec 管理 **WHAT**（需求提案、Spec 生命周期、归档），Superpowers 管理 **HOW**（技术设计、规划、执行、收尾），Comet 将两者串联为五阶段自动化流水线。一条命令从 idea 到归档，支持断点续做。

## 核心特性

- **五阶段自动流水线**：Open → Design → Build → Verify → Archive，自动检测当前阶段并继续
- **断点恢复**：关闭 Claude Code 后 `/comet continue` 自动读取活跃 Spec，识别当前阶段继续执行
- **双预设路径**：`/comet-hotfix`（跳过头脑风暴）、`/comet-tweak`（跳过头脑风暴和完整计划）
- **可靠状态机**：通过 Shell 脚本（`comet-guard.sh`、`comet-state.sh`）管理状态转换，而非依赖 Agent 记忆 YAML
- **28 个 AI 平台支持**：Claude Code、Cursor、Codex、Windsurf、Cline、Gemini CLI、Kiro、GitHub Copilot 等
- **Schema 校验**：`comet-yaml-validate.sh` 验证 YAML 结构和字段值
- **归档自动化**：`comet-archive.sh` 一条命令完成状态验证、delta spec 同步、归档移动

## 五阶段工作流

| 阶段 | 命令 | 负责方 | 产出物 |
|------|------|--------|--------|
| 1. Open | `/comet-open` | OpenSpec | proposal.md、design.md、tasks.md |
| 2. Deep Design | `/comet-design` | Superpowers | Design Doc、delta spec |
| 3. Plan & Build | `/comet-build` | Superpowers | 实现计划、代码提交 |
| 4. Verify & Finish | `/comet-verify` | 两者 | 验证报告、分支处理 |
| 5. Archive | `/comet-archive` | OpenSpec | delta→main spec 同步、归档 |

## 状态管理架构

| 文件 | 管理方 | 用途 |
|------|--------|------|
| `.openspec.yaml` | OpenSpec | Spec 生命周期、变更元数据 |
| `.comet.yaml` | Comet | 工作流阶段、执行模式、验证状态 |

两个 YAML 文件解耦管理，状态转换通过脚本保证可靠性，Agent 只需读取状态无需手动编辑。

## 安装

```bash
npm install -g @rpamis/comet
cd your-project && comet init
```

`comet init` 自动检测已安装的 AI 平台，选择安装范围（项目级/全局），选择语言（英文/中文），部署 OpenSpec + Superpowers + Comet 三组 Skills。

## 技术实现亮点

- **嵌套 Skill 触发**：真正触发子 Skill（而非 Agent 模仿 Skill 写文件），Prompt 设计值得参考
- **多阶段自动流转**：核心流程自动触发 Skill，仅在用户选择节点手动确认
- **Shell 脚本保障状态**：不依赖 Agent 记忆复杂状态，脚本保证 YAML 正确性和断点恢复
- **路径穿越保护**：所有变更名称输入均有安全校验

## 亮点 / 个人评价

Comet 解决了 AI Agent 长任务开发中的核心痛点——状态丢失和流程断裂。OpenSpec 擅长需求管理但缺技术深度，Superpowers 擅长技术执行但缺状态持久化，两者结合形成了完整闭环。项目最大的工程价值在于用 Shell 脚本而非 Prompt 来管理状态转换，这是对"Agent 不可靠记忆"问题的务实解法。对想学习 Skill 组合和嵌套触发机制的开发者来说，这个项目是很好的参考。
