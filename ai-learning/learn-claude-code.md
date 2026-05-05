# Learn Claude Code — Agent Harness 工程实战教程

- **地址**：https://github.com/shareAI-lab/learn-claude-code
- **作者**：shareAI-lab
- **协议**：MIT
- **分类**：ai-learning

## 简介

一个从零到一教你构建 AI Agent Harness（智能体外壳）的渐进式教程。核心理念：**Agent 的智能来自模型训练，而非代码编排。工程师的工作是构建 Harness——模型运行的环境（工具、知识、上下文、权限）。**

项目以 Claude Code 为教学对象，通过 12 个递进式 Session，逐步反编译 Claude Code 的架构机制，从最简单的 Agent Loop 到完整的 Worktree 隔离执行。

## 核心思想

```
Agent = Model（智能）+ Harness（环境）
Harness = Tools + Knowledge + Observation + Action + Permissions
```

- **Agency 来自模型训练**，不是外部代码编排（if-else、节点图、Prompt 链）
- Prompt plumbing 不是 Agent，只是套了 LLM 外壳的 GOFAI
- 工程师的角色是 Harness Engineer：构建模型运行的世界

## 12 个递进式 Session

| Session | 主题 | 座右铭 |
|---------|------|--------|
| s01 | Agent Loop | 一个循环 + Bash 就够了 |
| s02 | Tool Use | 加一个工具就是加一个 handler |
| s03 | TodoWrite | 没有计划的 Agent 会漂移 |
| s04 | Subagents | 拆分大任务，每个子任务干净上下文 |
| s05 | Skills | 按需加载知识，不要预先注入 |
| s06 | Context Compact | 上下文会满，需要压缩策略 |
| s07 | Tasks | 大目标拆小任务，排序，持久化到磁盘 |
| s08 | Background Tasks | 慢操作后台运行，Agent 继续思考 |
| s09 | Agent Teams | 任务太大就委派给队友 |
| s10 | Team Protocols | 队友需要共享通信规则 |
| s11 | Autonomous Agents | 队友自己扫描看板、认领任务 |
| s12 | Worktree Isolation | 各自独立目录，互不干扰 |

## 核心代码模式

```python
def agent_loop(messages):
    while True:
        response = client.messages.create(model, system, messages, tools)
        messages.append({"role": "assistant", "content": response.content})
        if response.stop_reason != "tool_use":
            return
        results = [execute(block) for block in response.content if block.type == "tool_use"]
        messages.append({"role": "user", "content": results})
```

每个 Session 在此循环之上叠加一个 Harness 机制，循环本身不变。

## 快速开始

```bash
git clone https://github.com/shareAI-lab/learn-claude-code
cd learn-claude-code
pip install -r requirements.txt
cp .env.example .env   # 填入 ANTHROPIC_API_KEY
python agents/s01_agent_loop.py       # 从这里开始
python agents/s12_worktree_task_isolation.py  # 完整终点
```

还提供 Web 交互式学习平台（Next.js）和三语文档（英/中/日）。

## 关联项目

- **Kode CLI**：基于此教程的开源编码 Agent CLI，支持 GLM/MiniMax/DeepSeek 等开源模型
- **claw0**：姊妹教学仓库，在 Harness 核心之上增加 Heartbeat、Cron、IM 通道、记忆、人格系统，实现主动式 Agent

## 亮点 / 个人评价

- 观点犀利："Prompt plumbing 不是 Agent，只是套了 LLM 外壳的 shell script"
- 从底层原理出发，不是教你用框架，而是教你理解 Agent 的本质架构
- 12 步渐进设计精妙，每步一个概念一个座右铭，学习曲线平滑
- Python 代码可直接运行，理论与实践紧密结合
- 对 Harness Engineer 角色的定位清晰实用
