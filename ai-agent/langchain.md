# LangChain — Agent 工程平台

- **地址**：https://github.com/langchain-ai/langchain
- **官网**：https://www.langchain.com
- **文档**：https://docs.langchain.com
- **协议**：MIT
- **分类**：AI Agent

## 简介

LangChain 是构建 Agent 和 LLM 应用的框架，定位为 "Agent Engineering Platform"。它将可互操作的组件和第三方集成串联在一起，简化 AI 应用开发，同时在底层技术演进时保护已有投资。

## 核心价值

- **模型互操作性**：自由切换不同模型（OpenAI、Anthropic、Google 等），框架抽象层让切换零成本
- **实时数据增强**：通过丰富的集成库连接 LLM 到各类数据源和外部系统
- **快速原型开发**：模块化组件架构，快速构建和迭代 LLM 应用
- **生产级特性**：内置监控、评估和调试支持（通过 LangSmith）
- **灵活的抽象层级**：从高层 Chain 快速起步，到低层组件精细控制

## LangChain 生态

| 产品 | 定位 |
|------|------|
| **LangChain** | 核心框架，模型/嵌入/向量存储的标准接口 |
| **LangGraph** | 低层 Agent 编排框架，构建可控的 Agent 工作流 |
| **LangSmith** | Agent 评估、可观测性和调试平台 |
| **LangSmith Deployment** | 部署和扩展 Agent 的托管平台，支持长时间有状态工作流 |
| **Deep Agents** | 构建能规划、使用子 Agent、利用文件系统的复杂 Agent |

## 快速开始

```bash
pip install langchain
# 或
uv add langchain
```

```python
from langchain.chat_models import init_chat_model

model = init_chat_model("openai:gpt-5.4")
result = model.invoke("Hello, world!")
```

## 相关资源

- **LangChain.js**：JavaScript/TypeScript 版本 — https://github.com/langchain-ai/langchainjs
- **LangChain Academy**：官方免费课程 — https://academy.langchain.com
- **Chat LangChain**：与文档对话 — https://chat.langchain.com
- **社区论坛**：https://forum.langchain.com

## 亮点

LangChain 是 LLM 应用开发领域最流行的框架之一，GitHub Star 数在 AI 项目中名列前茅。它的核心优势在于 **丰富的集成生态**（几乎覆盖所有主流模型和工具）和 **分层设计**（从简单 Chain 到复杂 Agent 工作流都有对应抽象）。LangGraph 作为其 Agent 编排方案，支持循环、分支、持久化状态等复杂工作流模式，是构建生产级 Agent 应用的关键组件。
