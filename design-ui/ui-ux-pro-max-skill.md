# UI UX Pro Max Skill

- **地址**：https://github.com/nextlevelbuilder/ui-ux-pro-max-skill
- **官网**：https://uupm.cc
- **作者**：NextLevelBuilder
- **协议**：MIT
- **分类**：design-ui

## 简介

UI UX Pro Max 是一个 AI Skill，为 AI 编程助手提供专业级 UI/UX 设计智能。核心能力是 v2.0 的**设计系统生成器**——一个 AI 推理引擎，分析项目需求后自动生成完整的设计系统（风格、配色、字体、布局模式、反模式清单）。

## 核心特性

- **161 条行业推理规则**：覆盖 Tech/SaaS、金融、医疗、电商、服务、创意、生活方式等 161 个产品类型
- **67 种 UI 风格**：Glassmorphism、Claymorphism、Brutalism、Bento Grid、AI-Native UI、Liquid Glass、Spatial UI 等
- **161 套配色方案**：与产品类型 1:1 对应的行业专属配色
- **57 组字体搭配**：精选 Google Fonts 组合
- **25 种图表类型**：BI/Analytics 仪表盘推荐
- **99 条 UX 准则**：最佳实践、反模式、无障碍规则
- **15 种技术栈支持**：React、Next.js、Vue、Nuxt、Svelte、SwiftUI、Flutter、Angular、Laravel 等

## 设计系统生成流程

```
用户请求 -> 多域搜索（5 路并行：产品类型/风格/配色/页面模式/字体）
-> 推理引擎（BM25 排序 + 反模式过滤）
-> 完整设计系统输出（模式+风格+配色+字体+效果+反模式+交付检查清单）
```

## 安装

```bash
# Claude Code 插件市场
/plugin marketplace add nextlevelbuilder/ui-ux-pro-max-skill
/plugin install ui-ux-pro-max@ui-ux-pro-max-skill

# CLI 安装（支持 17+ AI 平台）
npm install -g uipro-cli
uipro init --ai claude      # Claude Code
uipro init --ai cursor      # Cursor
uipro init --ai all         # 所有平台
```

依赖 Python 3.x（用于搜索脚本）。

## 使用

自然语言触发，无需特殊命令：

```
Build a landing page for my SaaS product
Create a dashboard for healthcare analytics
Design a portfolio website with dark mode
```

支持高级命令直接生成设计系统，并可持久化到 `design-system/MASTER.md` 实现跨会话复用。

## 亮点 / 个人评价

- 推理引擎设计精巧：161 个行业分类 x 5 维度并行搜索，自动匹配最佳设计方案
- 反模式机制实用：自动提示"银行业不要用 AI 紫粉渐变"等行业禁忌
- 跨平台支持极广：17+ AI 编程助手，CLI 一键安装
- 设计系统持久化功能解决了 AI 生成 UI 风格不统一的痛点
- 免费开源，质量媲美商业设计系统工具
