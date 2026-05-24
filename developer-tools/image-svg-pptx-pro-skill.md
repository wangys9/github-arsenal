# Image-SVG-PPTX Pro Skill

- **地址**：https://github.com/kongzhecn/image-svg-pptx-pro-skill
- **作者**：kongzhecn
- **协议**：未声明
- **分类**：开发者工具

## 简介

Codex/Agent 环境下的图片转 PPT 技能。将 PPT 截图、学术图表、UI 设计稿、海报、报告页面等光栅图像，通过 SVG 中间层重建为高保真可编辑的 .pptx 文件。核心理念是"有用优先，而非理论可编辑"——文字、卡片、线条、表格等转可编辑元素，复杂照片、Logo、截图保留高清裁剪。

## 核心特性

- **SVG 中间层路线**：source image → layout plan → SVG → editable PPTX，SVG 作为稳定的中间表示，精确编码几何、排版、图像裁剪和矢量图元
- **语义布局计划**：通过 `layout_plan.json` 分解图像为语义层（文本、矢量元素、资源裁剪区），带 z-order 和可编辑意图标注
- **三种质量模式**：`balanced`（默认，核心文字可编辑）、`max_editable`（最大化可编辑元素）、`visual_locked`（保真优先）
- **智能资产裁剪**：复杂图片区域自动裁剪为独立资产，精确还原位置
- **QA 校验闭环**：自动生成视觉和可编辑性评估报告，不合格自动回溯修正
- **完整输出包**：pptx、svg、layout_plan.json、assets/、qa_report.md、可选 VBA 辅助宏

## 工作流程

1. **图像归一化**：预处理输入图像（矫正、裁剪、元数据提取）
2. **语义分解**：视觉推理生成 `layout_plan.json`，标注文本、矢量、裁剪区域及其可编辑意图
3. **资产裁剪**：从源图中裁剪复杂区域（Logo、截图、装饰图）
4. **SVG 生成**：基于布局计划生成高保真 SVG 中间文件
5. **PPTX 重建**：基于语义计划生成可编辑 PPTX（优先于 SVG 直接解析）
6. **QA 校验**：检查标题层级、文字正确性、对齐、颜色、可编辑性，不达标则回溯修正

## 设计原则

- 不强行拉伸文字匹配截图，用字号、字间距、行距近似
- 中文幻灯片优先可读性和正确性，而非强制字体匹配
- 无法辨认的文字不臆测，使用裁剪图回退并标记待审
- 复杂 Logo/图标不重绘，直接从源图裁剪精确定位

## 安装

```bash
# 复制到 Agent skills 目录
cp -r image-svg-pptx-pro-skill ~/.agents/skills/image-svg-pptx-pro

# 或项目内
cp -r image-svg-pptx-pro-skill <project>/.agents/skills/

# 安装 Python 依赖
pip install -r requirements.txt
```

## 亮点 / 个人评价

这个项目的设计理念很务实——"有用优先于理论可编辑"和"不臆测不可读文字"这两条原则，避免了 AI 生成 PPT 中常见的"看起来对但实际是错的"问题。SVG 中间层 + 语义布局计划的架构比直接 OCR 转 PPT 更可靠，因为 SVG 能精确编码几何和排版信息，而布局计划保留了语义意图。三种质量模式的设计也考虑了不同场景的需求差异。作为 Agent Skill 的形态也很轻量，直接集成到 Codex/Claude Code 工作流中使用。
