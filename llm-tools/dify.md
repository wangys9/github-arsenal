# Dify

- **地址**：https://github.com/langgenius/dify
- **官网**：https://dify.ai
- **团队**：LangGenius
- **协议**：Dify Open Source License（基于 Apache 2.0，含额外条款）
- **分类**：大模型工具
- **标签**：LLM 平台、AI Workflow、RAG、Agent、LLMOps

## 简介

开源 LLM 应用开发平台，提供可视化 AI 工作流编排、RAG 管道、Agent 构建、模型管理和可观测性等一站式能力，帮助开发者从原型快速走向生产。支持云服务和自部署两种使用方式。

## 核心特性

- **可视化 Workflow**：在画布上构建和测试 AI 工作流，支持拖拽编排
- **全面的模型支持**：无缝集成数百种 LLM（GPT、Mistral、Llama3 等），兼容 OpenAI API 格式的任意模型
- **Prompt IDE**：可视化提示词编写界面，支持模型性能对比、TTS 等附加功能
- **RAG 管道**：从文档摄入到检索的完整 RAG 能力，开箱支持 PDF、PPT 等常见格式的文本提取
- **Agent 能力**：基于 LLM Function Calling 或 ReAct 定义 Agent，内置 50+ 工具（Google Search、DALL·E、Stable Diffusion、WolframAlpha 等）
- **LLMOps**：监控和分析应用日志与性能，基于生产数据持续优化提示词、数据集和模型
- **Backend-as-a-Service**：所有功能均提供 API，可轻松集成到自有业务逻辑中

## 部署方式

| 方式 | 说明 |
|------|------|
| **Dify Cloud** | 官方托管服务，零配置上手，沙盒计划含 200 次 GPT-4 调用 |
| **Docker Compose** | 一行命令自部署（CPU >= 2 Core, RAM >= 4 GiB） |
| **Kubernetes** | 社区贡献多个 Helm Chart 和 YAML 方案 |
| **Terraform / CDK** | 一键部署到 Azure、GCP、AWS |

```bash
# Docker 快速启动
cd dify/docker
./dify-compose up -d
# 访问 http://localhost/install 初始化
```

## 可观测性集成

原生支持 Opik、Langfuse、Arize Phoenix 等可观测性平台，用于追踪和分析 LLM 应用性能。

## 亮点 / 个人评价

- **最活跃的 LLM 开发平台之一**：GitHub Star 数极高，社区活跃，迭代频繁
- **低门槛高上限**：非技术人员可通过可视化界面构建 AI 应用，开发者可通过 API 深度定制
- **全栈 LLMOps**：从提示词工程到生产监控的完整工具链
- **企业就绪**：提供 AWS Marketplace AMI、阿里云计算巢等一键部署方案
- **与国内生态兼容**：支持国内主流大模型厂商的 API
