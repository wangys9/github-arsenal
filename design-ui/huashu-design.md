# Huashu Design

- **地址**：https://github.com/alchaincyf/huashu-design
- **作者**：花叔 / Huasheng（[@AlchainHust](https://x.com/AlchainHust)）
- **协议**：个人免费使用，企业/商业用途需授权（$1,800/年 或 $3,500 一次性）
- **分类**：设计与 UI

## 简介

一句话描述需求，3-30 分钟交付产品级设计。支持 Claude Code、Cursor、Codex、OpenClaw 等多种 Agent。无需打开 Figma 或任何图形界面，纯对话驱动即可生成可交付的动画、原型、PPT、信息图。

核心理念：不是"对 AI 来说还不错"的质量，而是看起来像专业设计团队做的。

## 核心能力

| 能力 | 交付物 | 耗时 |
|------|--------|------|
| 交互原型（App/Web） | 单文件 HTML · 真实 iPhone 边框 · 可点击 · Playwright 验证 | 10-15 min |
| 演示文稿 | HTML 演示 + 可编辑 PPTX（保留文本框） | 15-25 min |
| 动效设计 | MP4（25fps/60fps）+ GIF + BGM | 8-12 min |
| 设计变体 | 3+ 方案并排对比 · 实时参数调整 | 10 min |
| 信息图/数据可视化 | 印刷级排版 · 导出 PDF/PNG/SVG | 10 min |
| 设计方向顾问 | 5 派系 × 20 哲学 · 推荐 3 个方向 · 并行生成 Demo | 5 min |
| 5 维专家评审 | 雷达图 + Keep/Fix/Quick Wins 行动清单 | 3 min |

## 核心机制

### 品牌资产协议（Core Asset Protocol）

处理品牌相关任务时强制执行的 5 步流程：询问 → 搜索官方渠道 → 按类型下载（每类 3 条兜底路径）→ 验证提取 → 冻结为 `brand-spec.md`。确保从真实资产出发，而非凭记忆猜测。

### 设计方向顾问

需求模糊时触发：从 5 大设计流派 × 20 种设计哲学中推荐 3 个差异化方向，并行生成 Demo，用户选择后进入设计流程。

### 初级设计师工作流

默认工作模式：批量提问 → 用占位符 + 推理注释先出草稿 → 尽早给用户看 → 填充真实内容 → 变体 → 微调，每步都展示。

### 反 AI 味规则

避免紫色渐变、emoji 图标、圆角+左边框、SVG 人形、Inter 字体等 AI 输出的视觉共性。使用 `text-wrap: pretty` + CSS Grid + 精选衬线展示字体 + oklch 色彩。

## 安装

```bash
npx skills add alchaincyf/huashu-design
```

使用示例：
```
"为 AI 心理学做一个 Keynote，给我 3 个风格方向选择"
"做一个番茄钟 App 的 iOS 原型 — 4 个页面，真正可点击"
"把这个逻辑做成 60 秒动画，导出 MP4 和 GIF"
```

## 亮点 / 个人评价

将 Claude Design 的品牌资产协议思想提炼为终端可用的 Skill，让设计工具层"消失"。Stage + Sprite 时间轴模型覆盖了大多数动效需求，HTML → 可编辑 PPTX 的转换是实用亮点。对不愿打开图形界面但又需要高质量设计输出的开发者来说，这是一个 80 分的解决方案。
