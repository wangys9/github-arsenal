# OpenDataLoader PDF — 面向 AI 的 PDF 解析器

- **地址**：https://github.com/opendataloader-project/opendataloader-pdf
- **官网**：https://opendataloader.org
- **协议**：Apache 2.0（2.0 之前版本为 MPL 2.0）
- **SDK**：Python、Node.js、Java
- **分类**：大模型工具

## 简介

OpenDataLoader PDF 是专为 AI/RAG 管线设计的 PDF 解析器，在基准测试中排名 #1（综合准确率 0.907）。支持从任意 PDF 中提取 Markdown、JSON（含边界框）和 HTML，同时具备 PDF 无障碍自动化能力——首个端到端生成 Tagged PDF 的开源工具。

## 核心能力

| 能力 | 说明 |
|------|------|
| 文本提取 | 正确阅读顺序（XY-Cut++ 算法）、标题层级、列表检测 |
| 表格提取 | 简单/复杂/无边框表格，Hybrid 模式准确率 0.928 |
| OCR | 支持 80+ 语言，扫描件 PDF 处理（需 300 DPI+） |
| 公式提取 | LaTeX 格式输出 |
| 图表描述 | AI 生成图表/图片描述（用于 RAG 搜索和 alt text） |
| 边界框 | 每个元素都有精确坐标，支持溯源引用 |
| AI 安全 | 自动过滤隐藏文本注入攻击、透明文字、页外内容 |
| Tagged PDF | 提取和生成 PDF 结构标签 |

## 两种模式

| 模式 | 速度 | 适用场景 |
|------|------|----------|
| **Local（默认）** | 0.015s/页，60+ 页/秒 | 标准数字 PDF，CPU 即可 |
| **Hybrid** | 0.46s/页 | 复杂表格、扫描件、公式、图表 |

Hybrid 模式将简单页面在本地 Java 引擎处理，复杂页面自动路由到 AI 后端，兼顾速度和准确率。

## 基准测试排名

| 引擎 | 综合 | 阅读顺序 | 表格 | 标题 |
|------|------|----------|------|------|
| **OpenDataLoader [hybrid]** | **0.907** | **0.934** | **0.928** | 0.821 |
| docling | 0.882 | 0.898 | 0.887 | **0.824** |
| marker | 0.861 | 0.890 | 0.808 | 0.796 |
| pymupdf4llm | 0.732 | 0.885 | 0.401 | 0.412 |

## 快速开始

```bash
pip install -U opendataloader-pdf
# Hybrid 模式（复杂 PDF）
pip install -U "opendataloader-pdf[hybrid]"
```

```python
import opendataloader_pdf

opendataloader_pdf.convert(
    input_path=["file1.pdf", "file2.pdf", "folder/"],
    output_dir="output/",
    format="markdown,json"
)
```

## 命令行使用

> [!info] 前置要求
> - Java 11+（核心引擎是 Java，Python/Node 只是封装层）
> - Python 3.10+

### 基础用法

```bash
# 安装
pip install -U opendataloader-pdf

# 处理文件（支持多文件和目录）
opendataloader-pdf file1.pdf file2.pdf folder/

# 指定输出格式
opendataloader-pdf file1.pdf --format json,markdown

# 静默模式
opendataloader-pdf file1.pdf --quiet
```

> [!example] 具体实例 — 将含空格/中文路径的 PDF 转为 Markdown
> ```bash
> # 方式一：本地模式（标准数字 PDF，无需服务端）
> opendataloader-pdf --format markdown "/Users/july/workspace/Vault/智慧实验室/仪器对接/浦江/AFS3000B  lis通信协议.pdf"
>
> # 方式二：混合模式（复杂表格/扫描件）
> # 终端 1 — 启动后端
> opendataloader-pdf-hybrid --port 5002
> # 终端 2 — 转换
> opendataloader-pdf --hybrid docling-fast --format markdown "/Users/july/workspace/Vault/智慧实验室/仪器对接/浦江/AFS3000B  lis通信协议.pdf"
>
> # 指定输出目录
> opendataloader-pdf --format markdown -o "/Users/july/workspace/output/" "/Users/july/.../xxx.pdf"
> ```

> [!tip] 批量建议
> 每次调用 `convert()` 或命令行都会启动一个 JVM 进程，因此应尽量在一次调用中传入所有文件，避免反复启动的开销。

### 混合模式（Hybrid）

混合模式将简单页面在本地处理（0.02s/页），复杂页面自动路由到 AI 后端。

```bash
# 安装混合模式依赖
pip install -U "opendataloader-pdf[hybrid]"

# 终端 1 — 启动后端服务
opendataloader-pdf-hybrid --port 5002

# 终端 2 — 处理 PDF
opendataloader-pdf --hybrid docling-fast file1.pdf file2.pdf folder/
```

### 扫描件 OCR

```bash
# 启用 OCR（适用于无可选文字的扫描 PDF）
opendataloader-pdf-hybrid --port 5002 --force-ocr

# 指定 OCR 语言（支持 en, ko, ja, ch_sim, ch_tra, de, fr, ar 等 80+ 语言）
opendataloader-pdf-hybrid --port 5002 --force-ocr --ocr-lang "ch_sim,en"
```

### 公式提取（LaTeX）

```bash
# 服务端启用公式增强
opendataloader-pdf-hybrid --enrich-formula

# 客户端必须使用 --hybrid-mode full，否则增强功能会被静默跳过
opendataloader-pdf --hybrid docling-fast --hybrid-mode full file1.pdf
```

输出示例：

```json
{
  "type": "formula",
  "page number": 1,
  "bounding box": [226.2, 144.7, 377.1, 168.7],
  "content": "\\frac{f(x+h) - f(x)}{h}"
}
```

### 图表/图片描述

```bash
# 服务端启用图片描述（使用 SmolVLM 256M 轻量视觉模型）
opendataloader-pdf-hybrid --enrich-picture-description

# 客户端
opendataloader-pdf --hybrid docling-fast --hybrid-mode full file1.pdf
```

### AI 安全过滤

```bash
# 启用敏感信息脱敏（邮箱、URL、电话号码 → 占位符）
opendataloader-pdf file1.pdf --sanitize
```

> [!note] 隐藏文本检测（`--filter-hidden-text`）默认关闭，因为需要逐页渲染 PDF，无法安全并行化。

### 场景速查

| 场景 | 服务端命令 | 客户端命令 |
|------|-----------|-----------|
| 标准数字 PDF | 无需服务端 | `opendataloader-pdf file.pdf` |
| 复杂/嵌套表格 | `opendataloader-pdf-hybrid --port 5002` | `opendataloader-pdf --hybrid docling-fast file.pdf` |
| 扫描件 OCR | `...--force-ocr` | `opendataloader-pdf --hybrid docling-fast file.pdf` |
| 多语言扫描件 | `...--force-ocr --ocr-lang "ch_sim,en"` | 同上 |
| 数学公式 | `...--enrich-formula` | `...--hybrid-mode full` |
| 图表描述 | `...--enrich-picture-description` | `...--hybrid-mode full` |

## LangChain 集成

```bash
pip install -U langchain-opendataloader-pdf
```

```python
from langchain_opendataloader_pdf import OpenDataLoaderPDFLoader

loader = OpenDataLoaderPDFLoader(
    file_path=["file1.pdf", "file2.pdf"],
    format="text"
)
documents = loader.load()
```

## PDF 无障碍自动化

首个开源端到端 Tagged PDF 生成工具，与 PDF Association 和 Dual Lab（veraPDF 开发者）合作开发：

- **审计**：检测 PDF 标签状态（已发布）
- **自动打标签**：布局分析 → Tagged PDF（2026 Q2，Apache 2.0 免费）
- **PDF/UA 导出**：转换为 PDF/UA-1/2 合规文件（企业版）
- **可视化编辑器**：审阅和修正标签（企业版）

## 亮点

OpenDataLoader PDF 在 PDF 解析领域做到了几个"唯一"：**唯一同时提供确定性地本地解析和 AI 混合模式**的开源工具、**唯一为每个元素提供边界框**的解析器、**唯一内置 Prompt 注入防护**、以及**首个端到端自动生成 Tagged PDF 的开源方案**。对于构建 RAG 管线的团队，它的 JSON 输出含元素坐标和页码，可以直接实现"点击溯源"的用户体验。
