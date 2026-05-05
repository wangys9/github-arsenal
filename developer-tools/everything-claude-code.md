# Everything Claude Code (ECC)

- **地址**：https://github.com/affaan-m/everything-claude-code
- **官网**：https://ecc.tools
- **作者**：Affaan Mustafa（@affaanmustafa）— Anthropic Hackathon Winner
- **协议**：MIT
- **Star**：140k+
- **分类**：developer-tools

## 简介

Everything Claude Code (ECC) 是 AI Agent Harness 的性能优化系统。不只是配置包，而是一套完整系统：48 个专业 Agent、183 个 Skills、79 个命令、Hooks、Rules、MCP 配置，经过 10+ 个月高强度日常使用验证。支持 Claude Code、Cursor、Codex、OpenCode、Gemini CLI 等多个 AI 编程平台。

## 核心组件

| 组件 | 数量 | 说明 |
|------|------|------|
| Agents | 48 | 专业子代理（planner、architect、tdd-guide、code-reviewer、security-reviewer 等） |
| Skills | 183 | 工作流定义和领域知识（TDD、安全、部署、成本优化等） |
| Commands | 79 | 传统斜杠命令（迁移中，优先使用 Skills） |
| Rules | 34 | 多语言编码规范（common + typescript + python + golang + swift + php） |
| Hooks | 20+ | 触发器自动化（session-start、post-edit、secret-detection 等） |
| MCP Servers | 14 | GitHub、Context7、Exa、Playwright 等 |

## 跨平台支持

| 平台 | Agents | Skills | Hooks | Rules |
|------|--------|--------|-------|-------|
| Claude Code | 48 | 183 | 8 types | 34 |
| Cursor IDE | Shared | Shared | 15 types | 34 |
| Codex CLI | Shared | 30 | - | Instruction |
| OpenCode | 12 | 37 | 11 types | 13 |

关键架构决策：根目录 AGENTS.md 是通用跨工具文件，Cursor 通过 DRY adapter 模式复用 Claude Code 的 Hook 脚本。

## 安装

```bash
# 插件安装（推荐）
/plugin marketplace add https://github.com/affaan-m/everything-claude-code
/plugin install everything-claude-code@everything-claude-code

# 手动安装 Rules（插件不自动分发 rules）
cp -r rules/common ~/.claude/rules/
cp -r rules/typescript ~/.claude/rules/
```

## 生态工具

- **AgentShield**：安全审计工具，1282 测试，102 规则，支持 Opus 红蓝对抗扫描
- **Continuous Learning v2**：基于 Instinct 的自动学习系统，支持导入/导出/演化
- **NanoClaw v2**：模型路由、Skill 热加载、会话管理
- **Dashboard GUI**：Tkinter 桌面应用，可视化浏览所有 ECC 组件
- **ECC 2.0 Alpha**：Rust 控制平面原型

## Token 优化建议

```json
{
  "model": "sonnet",
  "env": {
    "MAX_THINKING_TOKENS": "10000",
    "CLAUDE_AUTOCOMPACT_PCT_OVERRIDE": "50",
    "CLAUDE_CODE_SUBAGENT_MODEL": "haiku"
  }
}
```

保持 MCP < 10 个、活跃工具 < 80 个，避免上下文窗口缩水。

## 亮点 / 个人评价

- 140k+ Star 的现象级项目，AI 编程工具生态的基础设施
- 跨平台设计极具野心：一套 Skill 在 4+ AI 编程工具中运行
- 从实用经验中提炼的 Token 优化建议极具参考价值
- AgentShield 的 Opus 红蓝对抗安全扫描是独特创新
- 社区驱动，170+ 贡献者，迭代速度极快
