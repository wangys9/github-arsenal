# Prompt Optimizer

- **地址**：https://github.com/linshenkx/prompt-optimizer
- **在线体验**：https://prompt.always200.com
- **协议**：AGPL-3.0（允许商用但不可闭源）
- **分类**：大模型工具

## 简介

一款强大的 AI 提示词优化工具，帮助用户写出更好的 Prompt，提升 AI 输出质量。支持 Web 应用、桌面应用、Chrome 扩展和 Docker 四种使用方式，纯前端处理，数据不经过中间服务器。

## 核心能力

- **一键优化**：多轮迭代优化 Prompt，提升 AI 响应准确度
- **双模式优化**：支持系统提示词（System Prompt）和用户提示词（User Prompt）两种优化模式
- **分析与评估**：支持分析、单结果评估、多结果对比评估，判断 Prompt 是否真正改进
- **图片生成**：支持文生图（T2I）、图生图（I2I）、多图生成，集成 Gemini、Seedream 等模型
- **Prompt 花园**：发现、导入、收藏优质 Prompt，带版本历史和可复现示例
- **高级测试模式**：上下文变量管理、多轮对话测试、Function Calling 支持
- **MCP 协议**：支持 Model Context Protocol，可集成到 Claude Desktop 等 MCP 兼容应用

## 多模型支持

OpenAI、Gemini、DeepSeek、智谱 AI、SiliconFlow、MiniMax，以及通过自定义 API 接入的任何 OpenAI 兼容模型（如 Ollama）。

## 部署方式

| 方式 | 说明 |
|------|------|
| 在线版 | 直接访问 prompt.always200.com |
| Vercel | 一键部署到自己的 Vercel |
| 桌面应用 | 无 CORS 限制，支持自动更新 |
| Chrome 扩展 | Chrome Web Store 安装 |
| Docker | `docker run -d -p 8081:80 linshen/prompt-optimizer` |

## MCP 集成

Docker 部署时 MCP Server 自动启动，提供三个工具：
- `optimize-user-prompt`：优化用户提示词
- `optimize-system-prompt`：优化系统提示词
- `iterate-prompt`：根据特定需求迭代改进成熟 Prompt

## 安全架构

纯客户端处理，数据直接与 AI 服务商交互，绕过中间服务器。支持密码保护功能。

## 亮点 / 个人评价

功能覆盖全面——从 Prompt 优化到图片生成到 MCP 集成，一个工具串起整个 Prompt 工程工作流。纯前端架构是加分项，数据不经过第三方。桌面版解决了 CORS 痛点，Docker 一行命令即可部署。对经常写 Prompt 的开发者和产品经理来说，是值得常驻的工具。
