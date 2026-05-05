# Magic Resume

- **地址**：https://github.com/JOYCEQL/magic-resume
- **作者**：Siyue（@JOYCEQL）
- **协议**：Apache 2.0（个人免费，商业使用需获取商业授权）
- **分类**：design-ui

## 简介

Magic Resume 是一款现代化的在线简历编辑器，让创建专业简历变得简单且愉悦。基于 TanStack Start 和 Framer Motion 构建，支持实时预览、自定义主题和 AI 辅助写作。

## 核心特性

- **AI 辅助写作**：内置 AI 能力，支持自定义模型，帮助优化简历内容
- **实时预览**：编辑即所见，所见即所得
- **自定义主题**：支持多种主题风格，包括暗黑模式
- **导出 PDF**：一键导出为 PDF 格式
- **自动保存**：数据存储在本地，自动保存，隐私安全
- **自动一页**：智能调整简历内容为一页
- **多语言支持**：支持中英文界面
- **响应式设计**：适配各种屏幕尺寸

## 技术栈

| 类别 | 技术 |
|------|------|
| 框架 | TanStack Start |
| 语言 | TypeScript |
| 动画 | Framer Motion |
| 富文本编辑 | Tiptap |
| 样式 | Tailwind CSS |
| 状态管理 | Zustand |
| UI 组件 | Shadcn/ui |
| 图标 | Lucide Icons |

## 快速开始

```bash
git clone git@github.com:JOYCEQL/magic-resume.git
cd magic-resume
pnpm install
pnpm dev
# 访问 http://localhost:3000
```

也支持 Docker 部署：`docker compose up -d`

## 路线图

- [ ] AI 辅助写作、多语言支持、自定义模型、自动一页
- [ ] 更多简历模板、更多导出格式、导入 PDF/Markdown、在线简历托管

## 亮点 / 个人评价

- 隐私友好：数据全部本地存储，不上传服务器
- AI 集成：支持自定义模型接入，实用性高
- 视觉体验出色：Framer Motion 动画流畅，整体设计精致
- 商业使用需授权，个人使用完全免费
