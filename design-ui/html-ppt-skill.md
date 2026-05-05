# html-ppt-skill — HTML PPT Studio

- **地址**：https://github.com/lewislulu/html-ppt-skill
- **作者**：lewis (sudolewis@gmail.com)
- **协议**：MIT
- **分类**：设计与 UI

## 简介

一个面向 AI Agent 的 HTML 演示文稿生成技能（AgentSkill）。纯静态 HTML/CSS/JS 实现，无需构建步骤，即可生成专业级演示文稿。内置 **36 套主题**、**15 套完整模板**、**31 种页面布局**、**47 种动画效果**（27 CSS + 20 Canvas FX），以及像素级精确的**演讲者模式**。

## 核心特性

- **36 套主题**：涵盖极简、杂志风、赛博朋克、小红书白底、Glassmorphism、日式极简等风格，切换一个 `<link>` 即可换肤
- **15 套完整模板**：8 套从真实场景提取（小红书杂志风、蓝图架构风、终端 Cyberpunk 等），7 套通用场景（路演、产品发布、技术分享、周报、课程等）
- **31 种页面布局**：封面、目录、时间线、思维导图、甘特图、架构图、数据图表（柱/线/饼/雷达）等
- **47 种动画**：27 种 CSS 动画（淡入、打字机、霓虹发光、3D 翻转等）+ 20 种 Canvas 特效（粒子爆发、烟花、矩阵雨、知识图谱、星系旋转等）
- **演讲者模式**：按 `S` 键弹出专用窗口，包含当前幻灯片、下一页预览、逐字稿、计时器四个可拖拽磁吸卡片，通过 `BroadcastChannel` 与观众窗口实时同步
- **零构建**：纯静态文件，仅 CDN 引入字体和可选的 highlight.js / chart.js

## 安装

```bash
npx skills add https://github.com/lewislulu/html-ppt-skill
```

安装后，支持 AgentSkills 的 Agent 可通过自然语言指令生成演示文稿：

> "做一份 8 页的技术分享 slides，用 cyberpunk 主题"
> "turn this outline into a pitch deck"

也可手动使用：

```bash
./scripts/new-deck.sh my-talk          # 创建新演示
open templates/theme-showcase.html     # 浏览所有主题
./scripts/render.sh deck.html 12       # 渲染为 PNG
```

## 快捷键

| 按键 | 功能 |
|------|------|
| `← → Space` | 翻页 |
| `F` | 全屏 |
| `S` | 演讲者模式 |
| `N` | 快速笔记 |
| `O` | 幻灯片总览 |
| `T` | 切换主题 |

## 技术架构

- **设计系统**：Token 驱动，所有颜色、圆角、阴影、字体决策集中在 `base.css` + 主题文件中
- **预览隔离**：每个主题/布局预览使用独立 `<iframe>`，互不干扰
- **Canvas FX 运行时**：`fx-runtime.js` 在幻灯片进入时自动初始化 `[data-fx]` 特效
- **中英文优先**：预置 Noto Sans SC / Noto Serif SC 字体

## 亮点 / 个人评价

这是目前见过的最完整的 HTML 演示文稿生成工具。不同于 Reveal.js 等框架聚焦于开发者手动编写，它的定位是让 AI Agent 直接产出设计感强的演示文稿——36 套主题覆盖了从严肃商务到潮酷视觉的各种场景。演讲者模式的设计尤其出色，通过 iframe 隔离实现了像素级精确的预览同步。对于需要快速生成演示文稿的 AI 工作流来说，非常实用。
