# AI Website Cloner Template

- **地址**：https://github.com/JCodesMore/ai-website-cloner-template
- **协议**：MIT
- **分类**：开发者工具

## 简介

一个可复用的 Next.js 项目模板，配合 AI 编程 Agent 一键逆向克隆任意网站。指向目标 URL，运行 `/clone-website` 命令，AI Agent 会自动截图、提取设计 Token、编写组件规格、并行构建每个页面区块，最终生成干净的 Next.js 代码。推荐使用 Claude Code + Opus 4.6。

## 核心流程

| 阶段 | 内容 |
|------|------|
| 侦察 | 截图、设计 Token 提取、交互扫描（滚动/点击/悬停/响应式） |
| 基础搭建 | 更新字体、颜色、全局样式，下载所有资源 |
| 组件规格 | 编写详细规格文件（`docs/research/components/`），包含精确 CSS 计算值 |
| 并行构建 | 在 git worktree 中为每个区块/组件分派独立构建 Agent |
| 组装 & QA | 合并 worktree、组装页面、与原站做视觉对比 |

## 支持的 AI Agent

13 个平台：Claude Code（推荐）、Codex CLI、OpenCode、GitHub Copilot、Cursor、Windsurf、Gemini CLI、Cline、Roo Code、Continue、Amazon Q、Augment Code、Aider。

## 技术栈

| 技术 | 用途 |
|------|------|
| Next.js 16 | App Router、React 19、TypeScript strict |
| shadcn/ui | Radix 原语 + Tailwind CSS v4 |
| Tailwind CSS v4 | oklch 设计 Token |
| Lucide React | 图标（克隆时替换为提取的 SVG） |

## 使用方式

```bash
git clone https://github.com/JCodesMore/ai-website-cloner-template.git my-clone
cd my-clone
npm install
claude --chrome           # 启动 Claude Code
# 在 Claude Code 中运行：
/clone-website https://example.com
```

需要 Node.js 24+，AI Agent 需具备浏览器能力（`--chrome` 模式）。

## 适用场景

- **平台迁移**：从 WordPress/Webflow/Squarespace 迁移到现代 Next.js
- **源码丢失恢复**：网站在线但仓库丢失，用现代技术栈重建
- **学习**：拆解生产网站的布局、动画、响应式实现方式

## 项目结构

```
src/
  app/              # Next.js 路由
  components/       # React 组件
    ui/             # shadcn/ui 原语
  lib/utils.ts      # 工具函数
  types/            # TypeScript 接口
  hooks/            # 自定义 React Hooks
public/
  images/           # 从目标站下载的图片
  videos/           # 从目标站下载的视频
docs/
  research/         # 提取输出和组件规格
  design-references/ # 截图
```

## 亮点 / 个人评价

把"克隆网站"这个复杂任务拆解成清晰的流水线：侦察 → 规格 → 并行构建 → QA。每个构建 Agent 收到的是精确的 `getComputedStyle()` 值、交互模型、多状态内容和响应式断点，而不是模糊的描述。支持 13 个 AI 编程平台，覆盖面广。对需要从旧平台迁移到 Next.js 的团队，或想学习现代网站实现的开发者来说，是一个非常实用的工具。项目也明确声明了使用边界（禁止钓鱼、冒充等）。
