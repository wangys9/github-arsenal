# Fireworks Tech Graph

- **地址**：https://github.com/yizhiyanhua-ai/fireworks-tech-graph
- **npm**：@yizhiyanhua-ai/fireworks-tech-graph
- **协议**：MIT
- **分类**：developer-tools

## 简介

Fireworks Tech Graph 是一个 Claude Code Skill，用自然语言描述系统架构即可生成可出版的 SVG + PNG 技术图表。无需手动画图、无需写 DSL 语法，直接用中英文描述即可秒级出图。

## 核心特性

- **7 种视觉风格**：Flat Icon（默认）、Dark Terminal、Blueprint、Notion Clean、Glassmorphism、Claude Official、OpenAI Official
- **14 种 UML 图表**：完整支持类图、组件图、部署图、序列图、状态机图、ER 图等全部 UML 类型
- **AI/Agent 领域图表**：内置 RAG Pipeline、Agentic Search、Mem0 Memory、Multi-Agent、Tool Call Flow 等模式
- **语义化形状**：LLM = 双边框矩形、Agent = 六边形、Vector Store = 带环圆柱体
- **语义化箭头**：颜色 + 虚线模式编码含义（写入/读取/异步/循环）
- **40+ 产品图标**：OpenAI、Anthropic、Pinecone、Kafka、PostgreSQL 等品牌色图标
- **高清输出**：SVG 源文件 + 1920px PNG（2x Retina）

## 风格速查

| 风格 | 背景 | 适用场景 |
|------|------|----------|
| Flat Icon | 白色 | 博客、PPT、文档 |
| Dark Terminal | 深色 | GitHub README、技术文章 |
| Blueprint | 深蓝 | 架构文档、工程图纸 |
| Notion Clean | 白色极简 | Notion、Confluence、Wiki |
| Glassmorphism | 深色渐变 | 产品官网、Keynote |
| Claude Official | 暖白 [[f8f6f3]] | Anthropic 风格图表 |
| OpenAI Official | 纯白 | OpenAI 风格图表 |

## 安装

```bash
# 作为 Claude Code Skill 安装
npx skills add yizhiyanhua-ai/fireworks-tech-graph

# 依赖 rsvg-convert（macOS）
brew install librsvg
```

## 使用示例

```
Draw a RAG pipeline flowchart
Generate an Agentic Search architecture diagram, dark terminal style
画一个微服务架构图，使用 Blueprint 风格
```

技能自动识别触发词：generate diagram / draw diagram / create chart / visualize / architecture diagram 等。

## 亮点 / 个人评价

- 解决了"描述系统 -> 得到图表"的核心需求，比 Mermaid 和 draw.io 更自然
- 7 种风格覆盖主流场景，Claude/OpenAI 官方风格是独特卖点
- 语义化形状和箭头系统设计精巧，图表信息密度高
- 40+ 产品图标让架构图看起来像官方文档出品
- 作为 Claude Code Skill 集成，使用体验无缝
