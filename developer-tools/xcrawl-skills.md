# XCrawl Skills

- **地址**：https://github.com/xcrawl-api/xcrawl-skills
- **官网**：https://dash.xcrawl.com/
- **作者/团队**：xcrawl-api
- **协议**：未明确标注
- **分类**：developer-tools

## 简介

XCrawl Skills 是一套面向 AI Agent 的可复用 Skill 定义，让 Agent 通过标准化 API 调用完成网页数据采集工作流。基于 XCrawl 网页数据基础设施（搜索、抓取、URL 映射、站点爬取），提供 5 个生产级 Skill，每个 Skill 包含完整的应用场景、请求/响应参数文档、cURL 和 Node.js 示例代码。

## Skill 目录

| Skill | 用途 |
|-------|------|
| `xcrawl` | 默认入口，直接查询和单 URL 提取 |
| `xcrawl-scrape` | 单页面提取和结构化数据工作流 |
| `xcrawl-map` | 站点 URL 发现和范围规划 |
| `xcrawl-crawl` | 批量站点爬取和异步结果处理 |
| `xcrawl-search` | 基于查询的发现，支持地区/语言控制 |

## 核心 API 端点

- `POST /v1/scrape` + `GET /v1/scrape/{id}` — 同步/异步单页抓取
- `POST /v1/map` — 站点 URL 映射
- `POST /v1/crawl` + `GET /v1/crawl/{id}` — 批量爬取（支持深度和数量限制）
- `POST /v1/search` — 搜索引擎式查询

## 快速开始

```bash
# 注册获取 API Key，赠送 1000 免费额度
# 配置本地密钥
mkdir -p ~/.xcrawl && echo '{"XCRAWL_API_KEY":"<your_key>"}' > ~/.xcrawl/config.json

# Agent 自动读取配置，直接调用 Skill
```

每个 Skill 文件（`skills/*/SKILL.md`）包含场景说明、参数文档和可执行示例，Agent 可直接使用。

## 跨 Agent 契约

统一的输入/输出标准化接口：
- **输入**：`goal`（目标）、`inputs`（参数）、`constraints`（约束）、`credentials_ref`（凭证）、`runtime_context`（运行时上下文）
- **输出**：`status`（状态）、`request_payload`（请求体）、`raw_response`（原始响应）、`task_ids`（异步任务 ID）、`error`（错误信息）

默认透传模式：直接返回上游 API 响应，不做额外转换。

## 亮点 / 个人评价

这是 API 服务商为 AI Agent 生态提供 Skill 定义的一个典型范例。将 API 能力封装为标准 SKILL.md 格式，Agent 可以即插即用。对于需要网页数据采集（搜索、抓取、爬取）的 Agent 工作流来说，省去了自己编写爬虫的麻烦，直接通过 API 调用获得结构化结果。1000 免费额度的起步门槛较低，适合评估和轻量使用。项目结构清晰，可作为"如何为 API 产品编写 AI Agent Skill"的参考模板。
