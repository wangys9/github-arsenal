# Claude-Mem

- **地址**：https://github.com/thedotmack/claude-mem
- **作者**：Alex Newman（@thedotmack）
- **协议**：AGPL-3.0
- **分类**：developer-tools

## 简介

Claude-Mem 是专为 Claude Code 构建的持久化记忆压缩系统。通过自动捕获工具使用观察、生成语义摘要并在未来会话中注入，使 Claude 能够跨会话保持项目知识的连续性。

## 核心特性

- **持久化记忆**：上下文在会话之间自动保存和恢复
- **渐进式披露**：分层记忆检索，带 Token 消耗可视化，约 10x Token 节省
- **混合搜索**：Chroma 向量数据库 + SQLite FTS5，支持语义和关键词混合检索
- **MCP 搜索工具**：3 层搜索工作流（search → timeline → get_observations）
- **Web 查看器**：实时记忆流 UI（http://localhost:37777）
- **技能搜索**：mem-search 技能，自然语言查询项目历史
- **隐私控制**：`<private>` 标签排除敏感内容
- **多语言支持**：内置中文、日文等模式
- **多平台**：支持 Claude Code、Gemini CLI、OpenCode
- **Beta 频道**：Endless Mode 等实验性功能

## 架构

| 组件 | 说明 |
|------|------|
| 5 个生命周期 Hook | SessionStart、UserPromptSubmit、PostToolUse、Stop、SessionEnd |
| Worker Service | HTTP API（端口 37777）+ Web UI，Bun 管理 |
| SQLite 数据库 | 存储会话、观察记录、摘要 |
| Chroma 向量库 | 语义搜索 + 关键词搜索的混合检索 |
| mem-search Skill | 自然语言查询 + 渐进式披露 |

## 安装

```bash
# 一键安装
npx claude-mem install

# Gemini CLI
npx claude-mem install --ide gemini-cli

# 插件市场安装
/plugin marketplace add thedotmack/claude-mem
/plugin install claude-mem
```

要求 Node.js >= 18，Bun 和 uv 会自动安装。

## 亮点 / 个人评价

- 解决了 Claude Code 跨会话失忆的核心痛点
- 渐进式披露设计精妙，在记忆完整性和 Token 成本之间取得平衡
- 架构完善：Hook 捕获 -> Worker 处理 -> 向量索引 -> 智能检索，全链路自动化
- 社区活跃，文档齐全（docs.claude-mem.ai）
- 支持 30+ 种语言的 README，国际化程度高
