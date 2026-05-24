# PPT Master

- **地址**：https://github.com/hugohe3/ppt-master
- **官网**：https://www.hehugo.com
- **作者**：Hugo He（CPA · CPV · Consulting Engineer）
- **协议**：MIT
- **分类**：开发者工具

## 简介

PPT Master 是一个 AI 驱动的演示文稿生成工具（harness），能在 AI IDE（Claude Code、Cursor、VS Code Copilot 等）中从 PDF、DOCX、URL、Markdown 等素材直接生成**原生可编辑的 .pptx 文件**。输出的每个形状、文本框、图表都可以在 PowerPoint 中直接点击编辑，不是图片拼凑。

核心理念：`harness + model = agent`——工具控制工作流，模型决定质量上限。推荐使用 Claude Opus/Sonnet（大上下文窗口）+ `gpt-image-2`（AI 图片生成）获得最佳效果。

## 核心特性

- **原生可编辑 PPTX**：输出真实的 DrawingML 形状、文本框、图表，非图片导出
- **实时预览与可视化编辑**：生成过程中自动打开浏览器预览，点击元素可添加批注，AI 重新生成后导出
- **模板复制**：传入任意 .pptx 文件，通过 `/create-template` 提取主题色、字体、母版布局，生成可复用的私有模板
- **动画与转场**：支持页面转场和逐元素入场动画（真实 OOXML，非嵌入视频），PowerPoint/Keynote 原生播放
- **旁白与视频导出**：TTS 生成每页旁白（90+ 语言），嵌入 PPTX 后由 PowerPoint 导出 MP4 视频
- **语音克隆**：支持 ElevenLabs / MiniMax / Qwen / CosyVoice 等语音克隆服务
- **多平台支持**：Claude Code、Cursor、VS Code Copilot、Codex CLI、Aider 等任意具备 Agent 能力的工具
- **数据本地**：除 AI 模型通信外，整个流程在本地运行

## 与同类工具的区别

| 类别 | 输出方式 | 可编辑性 |
|------|----------|----------|
| 模板填充 | 固定模板生成 PPTX | 受模板限制 |
| 图片式 | 每页一张大图打包为 PPTX | 不可编辑 |
| HTML 演示 | Web 页面 | 不是 PPTX |
| **PPT Master（原生可编辑）** | **真实 DrawingML 形状** | **每个元素可点击编辑** |

## 技术架构

- **语言**：Python 3.10+
- **工作流**：内容分析 → 设计规格确认 → SVG 生成 → PPTX 导出（python-pptx）
- **图片获取**：AI 生成（gpt-image-2）或 Web 搜索（Pexels/Pixabay/Openverse）
- **输出格式**：PPT 16:9、小红书、微信等 10+ 画布格式

## 安装与使用

```bash
# 克隆仓库
git clone https://github.com/hugohe3/ppt-master.git
cd ppt-master

# 安装依赖（唯一前置条件：Python 3.10+）
pip install -r requirements.txt
```

在 AI IDE 中打开项目，直接对话：

```
You: Please create a PPT from projects/q3-report/sources/report.pdf
```

AI 会先确认设计规格（模板、格式、页数等），然后自动完成内容分析、视觉设计、SVG 生成和 PPTX 导出。

## 亮点 / 个人评价

PPT Master 解决了一个核心痛点：大多数 AI 生成 PPT 的工具输出的是图片或受限模板，无法二次编辑。它通过 SVG 中间层 + python-pptx 导出，实现了真正的原生 PowerPoint 形状输出。作为 IDE 插件/Skill 运行的设计也很巧妙——用户无需学习新工具，在已有的 AI 编程环境中即可完成 PPT 生成。模板复制功能进一步降低了设计门槛，任何高质量参考 PPT 都能变成私有模板复用。
