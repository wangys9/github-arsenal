# Free Claude Code

- **地址**：https://github.com/Alishahryar1/free-claude-code
- **协议**：MIT
- **分类**：开发者工具

## 简介

一个本地代理服务器，将 Claude Code 的 Anthropic API 流量路由到 NVIDIA NIM、OpenRouter、DeepSeek、LM Studio、llama.cpp 或 Ollama 等后端。保持 Claude Code 客户端协议不变，让你自由选择免费、付费或本地模型。

## 核心能力

- **即插即用代理**：Claude Code 的 API 调用直接路由到选择的模型后端
- **六种后端**：NVIDIA NIM、OpenRouter、DeepSeek、LM Studio、llama.cpp、Ollama
- **按模型级别路由**：Opus/Sonnet/Haiku/Fallback 可分别指向不同后端
- **原生 /model 选择器**：代理暴露 `/v1/models` 端点，Claude Code 内可直接切换模型
- **流式输出 & 工具调用**：完整支持 thinking block、tool use、SSE 流式传输
- **Discord/Telegram 机器人**：可选的远程编码会话包装器
- **语音笔记**：可选的本地 Whisper 或 NVIDIA NIM 转录

## 支持的后端

| 后端 | 传输协议 | 需要 Key |
|------|---------|---------|
| NVIDIA NIM | OpenAI chat 转换 | 免费 API Key |
| OpenRouter | Anthropic Messages | API Key（有免费模型） |
| DeepSeek | Anthropic Messages | API Key |
| LM Studio | Anthropic Messages | 无（本地） |
| llama.cpp | Anthropic Messages | 无（本地） |
| Ollama | Anthropic Messages | 无（本地） |

## 安装使用

```bash
# 克隆并配置
git clone https://github.com/Alishahryar1/free-claude-code.git
cd free-claude-code
cp .env.example .env
# 编辑 .env 选择后端和模型

# 启动代理
uv run uvicorn server:app --host 0.0.0.0 --port 8082

# 启动 Claude Code（指向代理）
ANTHROPIC_AUTH_TOKEN="freecc" ANTHROPIC_BASE_URL="http://localhost:8082" claude
```

也支持 VS Code 扩展和 JetBrains ACP，通过环境变量 `ANTHROPIC_BASE_URL` 指向代理即可。

## 按模型级别混合路由

```dotenv
MODEL_OPUS="nvidia_nim/moonshotai/kimi-k2.5"
MODEL_SONNET="open_router/deepseek/deepseek-r1-0528:free"
MODEL_HAIKU="lmstudio/unsloth/GLM-4.7-Flash-GGUF"
MODEL="nvidia_nim/z-ai/glm4.7"
```

## 技术架构

```
Claude Code CLI / IDE
        ↓ Anthropic Messages API
Free Claude Code proxy (:8082)
        ↓ provider-specific adapter
NIM / OpenRouter / DeepSeek / LM Studio / llama.cpp / Ollama
```

FastAPI 暴露 Anthropic 兼容路由，代理负责 thinking block、tool call、token usage 的格式标准化，以及将请求优化（部分 Claude Code 探针请求本地直接应答）。

## 亮点 / 个人评价

解决了一个实际问题——不付 Anthropic 订阅费也能用 Claude Code。代理层做得很干净，保持了 Claude Code 原生体验不变。按模型级别路由的设计很灵活，可以把重度任务走付费模型、轻量任务走免费模型。对想体验 Claude Code 但不想订阅的用户来说是最直接的方案。
