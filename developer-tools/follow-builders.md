# Follow Builders

- **地址**：https://github.com/zarazhangrui/follow-builders
- **作者**：Zara Zhang
- **协议**：MIT
- **分类**：开发者工具

## 简介

一个 AI Agent Skill（支持 Claude Code 和 OpenClaw），追踪 25 位顶尖 AI Builder 的动态——包括研究员、创始人、产品经理和工程师——将他们在 X/Twitter、播客和官方博客上的内容整理成每日/每周摘要，推送到 Telegram、Discord、WhatsApp 等消息应用。核心理念：关注真正在做事的 Builder，而非重复他人观点的网红。

## 核心功能

- **多源内容聚合**：自动抓取 X/Twitter 动态、YouTube 播客转录、官方博客文章
- **AI 摘要生成**：用 AI 将原始内容重写为精炼摘要
- **定时推送**：支持每日或每周定时发送摘要到消息应用
- **多语言**：支持英文、中文或双语输出
- **对话式配置**：通过自然语言对话完成设置，无需编辑配置文件
- **可自定义摘要风格**：通过对话或编辑 prompt 文件调整摘要风格

## 信息源

### 播客（6 个）
Latent Space、Training Data、No Priors、Unsupervised Learning、The MAD Podcast、AI & I by Every

### AI Builder（25 位）
Andrej Karpathy、Swyx、Sam Altman、Amanda Askell、Alex Albert、Guillermo Rauch、Amjad Masad、Garry Tan、Kevin Weil 等

### 官方博客（2 个）
Anthropic Engineering、Claude Blog

## 安装

```bash
# Claude Code
git clone https://github.com/zarazhangrui/follow-builders.git ~/.claude/skills/follow-builders
cd ~/.claude/skills/follow-builders/scripts && npm install

# 使用
/follow-builders
```

无需 API Key，所有内容通过中央 Feed 统一获取。

## 工作原理

```
中央 Feed（每日更新） ← 博客抓取 + YouTube 转录 + X/Twitter API
        ↓
Agent 获取 Feed（一次 HTTP 请求，无需 API Key）
        ↓
AI 按用户偏好重写为摘要
        ↓
推送到 Telegram / Discord / WhatsApp / 邮件
```

## 自定义摘要

可通过对话调整（"让摘要更简洁"、"关注可操作的洞察"），或直接编辑 `prompts/` 下的 Markdown 文件：

- `summarize-podcast.md` — 播客摘要规则
- `summarize-tweets.md` — 推文摘要规则
- `summarize-blogs.md` — 博客摘要规则
- `digest-intro.md` — 整体摘要格式和语调
- `translate.md` — 翻译规则

## 隐私

- 无需 API Key，内容通过中央服务获取
- Telegram/邮件 Key 仅存储在本地 `~/.follow-builders/.env`
- 只读取公开内容
- 配置和偏好保留在本地

## 亮点 / 个人评价

"Follow builders, not influencers" 这个理念很有共鸣。信息源精心挑选了 25 位真正在 AI 领域做实事的人，而非泛泛的科技媒体。作为 AI Agent Skill 的形式很有前瞻性——不是独立应用，而是嵌入到你已有的 AI 编程工具中，通过对话完成所有配置。对想高效追踪 AI 行业动态又不想被信息噪音淹没的开发者来说，是一个省时省力的工具。
