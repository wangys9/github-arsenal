# PentAGI

- **地址**：https://github.com/vxcontrol/pentagi
- **协议**：AGPL-3.0
- **分类**：安全工具

## 简介

PentAGI（Penetration testing Artificial General Intelligence）是一个 AI 驱动的自动化渗透测试平台。面向信息安全专业人员、研究者和爱好者，提供全自主的渗透测试流程——AI Agent 自动决定并执行渗透步骤，在沙箱化的 Docker 环境中运行。

## 核心能力

- **全自主渗透测试**：AI Agent 自动规划并执行渗透测试步骤，支持执行监控和智能任务规划
- **20+ 专业安全工具**：内置 nmap、Metasploit、sqlmap 等主流渗透工具
- **专家团队分工**：委托系统分配专门的 AI Agent 处理研究、开发和基础设施任务
- **智能记忆系统**：长期存储研究成果和成功方法，供未来使用
- **知识图谱集成**：基于 Graphiti + Neo4j 的知识图谱，语义关系追踪和上下文理解
- **Web 情报收集**：内置浏览器抓取最新信息
- **多搜索引擎集成**：Tavily、Perplexity、DuckDuckGo、Google、Sploitus、Searxng 等
- **详细报告生成**：生成完整的漏洞报告和利用指南
- **Grafana/Prometheus 监控**：实时系统观察
- **REST + GraphQL API**：Bearer Token 认证，支持自动化集成

## 支持的 LLM

10+ Provider：OpenAI、Anthropic、Google AI/Gemini、AWS Bedrock、Ollama、DeepSeek、GLM、Kimi、Qwen，以及 OpenRouter、DeepInfra 等聚合器。支持 vLLM 本地部署。

## 技术架构

- **微服务架构**：支持水平扩展
- **Docker 沙箱**：所有操作在完全隔离的容器中执行
- **PostgreSQL + pgvector**：命令和输出持久化存储，向量搜索
- **智能容器管理**：根据任务需求自动选择 Docker 镜像
- **Langfuse 集成**：LLM 可观测性仪表盘
- **OAuth 支持**：GitHub 和 Google OAuth 集成

## 快速部署

通过 Docker Compose 一键部署，配置环境变量即可启动。Web UI 提供系统管理和监控界面。

## 亮点 / 个人评价

将 AI Agent 能力与专业渗透测试工具链深度整合，实现了从信息收集到漏洞利用的全流程自动化。专家团队分工模式让不同 Agent 专注擅长领域，提高效率。知识图谱 + 智能记忆的组合使其能在多次测试中积累经验。对安全团队来说是一个强有力的自动化辅助工具，但需注意仅在授权环境下使用。
