# MarkItDown

- **地址**：https://github.com/microsoft/markitdown
- **作者/团队**：Microsoft AutoGen Team
- **协议**：MIT
- **分类**：大模型工具

## 简介

Microsoft 开源的轻量级 Python 工具，用于将多种文件格式转换为 Markdown，专为 LLM 和文本分析管线设计。支持 PDF、PPT、Word、Excel、图片、音频、HTML、ZIP 等格式，保留文档结构（标题、列表、表格、链接等），输出适合大模型消费的 Markdown 文本。

## 核心特性

- **多格式支持**：PDF、PowerPoint、Word、Excel、图片（EXIF + OCR）、音频（EXIF + 语音转录）、HTML、CSV/JSON/XML、ZIP、YouTube URL、EPub
- **结构保留**：转换时保留标题层级、列表、表格、链接等文档结构
- **LLM 增强**：可通过 OpenAI 兼容客户端对图片进行描述、对音频进行转录
- **Azure Document Intelligence**：集成微软 Azure 文档智能服务，提升 PDF 转换质量
- **插件系统**：支持第三方插件扩展（如 `markitdown-ocr` 插件，用 LLM Vision 做 OCR）
- **多种调用方式**：CLI 命令行、Python API、Docker

## 安装与使用

```bash
# 安装（含所有可选依赖）
pip install 'markitdown[all]'

# 仅安装特定格式支持
pip install 'markitdown[pdf, docx, pptx]'

# CLI 使用
markitdown path-to-file.pdf > document.md
markitdown path-to-file.pdf -o document.md

# 管道方式
cat path-to-file.pdf | markitdown
```

```python
# Python API
from markitdown import MarkItDown

md = MarkItDown(enable_plugins=False)
result = md.convert("test.xlsx")
print(result.text_content)
```

```python
# 使用 LLM 增强图片描述
from markitdown import MarkItDown
from openai import OpenAI

client = OpenAI()
md = MarkItDown(llm_client=client, llm_model="gpt-4o")
result = md.convert("example.jpg")
print(result.text_content)
```

## 可选依赖模块

| 模块 | 用途 |
|------|------|
| `[pptx]` | PowerPoint 文件 |
| `[docx]` | Word 文件 |
| `[xlsx]` / `[xls]` | Excel 文件 |
| `[pdf]` | PDF 文件 |
| `[outlook]` | Outlook 邮件 |
| `[az-doc-intel]` | Azure Document Intelligence |
| `[audio-transcription]` | 音频转录（WAV/MP3） |
| `[youtube-transcription]` | YouTube 视频转录 |

## 亮点 / 个人评价

- **与 MinerU 互补**：MinerU 侧重高精度 PDF 解析，MarkItDown 覆盖格式更广（PPT、Word、Excel、音频、视频等），适合作为 LLM 数据预处理的万能转换器
- **设计哲学清晰**：输出面向 LLM 消费而非人类阅读，token 效率高
- **插件生态**：第三方可通过 `#markitdown-plugin` 标签发布插件，扩展性强
- **Microsoft 出品**：由 AutoGen 团队维护，质量和持续性有保障
- **安全注意**：`convert()` 方法较宽松（支持本地/远程/流），在不可信环境中应使用更窄的 `convert_local()` / `convert_stream()` 方法
