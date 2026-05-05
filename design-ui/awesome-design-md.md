# Awesome DESIGN.md — AI Agent UI 设计系统文档集合

- **地址**：https://github.com/VoltAgent/awesome-design-md
- **官网**：https://getdesign.md
- **协议**：MIT
- **分类**：设计与 UI

## 简介

Awesome DESIGN.md 是一个精心策划的 DESIGN.md 文件集合，灵感来源于真实开发者网站。DESIGN.md 是 Google Stitch 引入的新概念——一种纯文本设计系统文档，AI Agent 可以读取它来生成一致的 UI。

核心理念：**把 DESIGN.md 复制到项目根目录，告诉 AI Agent "照着这个风格做"，就能得到像素级精准的 UI。**

## 什么是 DESIGN.md

| 文件 | 谁读它 | 定义什么 |
|------|--------|----------|
| `AGENTS.md` | 编码 Agent | 如何构建项目 |
| `DESIGN.md` | 设计 Agent | 项目应该长什么样 |

DESIGN.md 就是 Markdown 文件，不需要 Figma 导出、JSON Schema 或特殊工具。LLM 天生擅长读 Markdown，所以无需额外解析或配置。

## 每个 DESIGN.md 的内容结构

| 章节 | 内容 |
|------|------|
| Visual Theme & Atmosphere | 基调、密度、设计哲学 |
| Color Palette & Roles | 语义化颜色名 + hex + 功能角色 |
| Typography Rules | 字体族、完整层级表 |
| Component Stylings | 按钮、卡片、输入框、导航及各状态 |
| Layout Principles | 间距系统、网格、留白哲学 |
| Depth & Elevation | 阴影系统、表面层级 |
| Do's and Don'ts | 设计约束和反模式 |
| Responsive Behavior | 断点、触摸目标、折叠策略 |
| Agent Prompt Guide | 快速颜色参考、可直接使用的提示词 |

每个站点还包含 `preview.html`（亮色预览）和 `preview-dark.html`（暗色预览），可视化展示色板、字体缩放、按钮、卡片等组件。

## 收录项目（69 个 DESIGN.md）

涵盖多个领域：

- **AI & LLM 平台**：Claude、Cohere、ElevenLabs、Minimax、Mistral AI、Ollama、OpenCode AI、Replicate、RunwayML、Together AI、VoltAgent、xAI
- **开发者工具 & IDE**：Cursor、Expo、Lovable、Raycast、Superhuman、Vercel、Warp
- **后端、数据库 & DevOps**：ClickHouse、Composio、HashiCorp、MongoDB、PostHog、Sanity、Sentry、Supabase
- **生产力 & SaaS**：Cal.com、Intercom、Linear、Mintlify、Notion、Resend、Zapier
- **设计 & 创意工具**：Airtable、Clay、Figma、Framer、Miro、Webflow
- **金融科技 & 加密**：Binance、Coinbase、Kraken、Mastercard、Revolut、Stripe、Wise
- **电商 & 零售**：Airbnb、Meta、Nike、Shopify、Starbucks
- **媒体 & 消费科技**：Apple、IBM、NVIDIA、Pinterest、PlayStation、SpaceX、Spotify、The Verge、Uber、Vodafone、WIRED
- **汽车**：BMW、Bugatti、Ferrari、Lamborghini、Renault、Tesla

## 使用方式

1. 从 [getdesign.md](https://getdesign.md) 选择一个站点的 DESIGN.md
2. 复制到项目根目录
3. 告诉 AI Agent 使用它生成 UI

## 亮点

这个项目降低了 AI 生成 UI 的门槛。以往要让 AI 输出符合特定设计风格的界面，需要大量描述和反复调整；现在直接指定一个 DESIGN.md（如 Linear 的极简风格、Stripe 的紫色渐变、Apple 的留白美学），AI 就能精准还原设计系统。对于没有专业设计师的团队，这是快速建立统一视觉语言的实用方案。
