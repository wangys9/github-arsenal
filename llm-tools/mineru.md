# MinerU — 高精度文档解析引擎

- **地址**：https://github.com/opendatalab/MinerU
- **官网**：https://mineru.net
- **团队**：OpenDataLab（InternLM 预训练团队）
- **协议**：MinerU Open Source License（基于 Apache 2.0）
- **分类**：大模型工具

## 简介

MinerU 是一个将 PDF、DOCX、PPTX、XLSX、图片、网页等文档转换为结构化 Markdown/JSON 的文档解析工具，专为 LLM、RAG、Agent 工作流设计。诞生于 [InternLM](https://github.com/InternLM/InternLM) 大模型预训练过程，专注于解决科学文献中的符号转换问题。

## 核心特性

- **全格式支持**：PDF、DOCX、PPTX、XLSX、图片原生解析
- **VLM + OCR 双引擎**：pipeline（无幻觉，支持纯 CPU）、vlm-engine（高精度，支持 vLLM/LMDeploy）、hybrid-engine（高精度 + 低幻觉）
- **109 语言 OCR**：自动检测扫描件/乱码 PDF 并启用 OCR
- **结构化输出**：公式 → LaTeX、表格 → HTML，保留标题/段落/列表结构，按人类阅读顺序输出
- **复杂布局处理**：多栏、跨页表格合并、自动去除页眉页脚页码
- **OmniDocBench 得分 90+**（VLM 引擎）、86+（pipeline 引擎）

## 三种解析后端

| 后端 | 特点 | 精度 | 硬件要求 |
|------|------|------|----------|
| pipeline | 兼容性好，支持纯 CPU | 86+ | 最低 4GB VRAM，16GB RAM |
| vlm-engine | 高精度 | 90+ | 最低 8GB VRAM |
| hybrid-engine | 高精度 + 低幻觉 | 90+ | 最低 8GB VRAM |
| http-client | 连接远程 OpenAI 兼容服务 | 取决于远端 | 仅需 2GB |

## 集成生态

- **AI 编码工具**：MCP Server（Cursor、Claude Desktop、Windsurf）
- **RAG 框架**：LangChain、LlamaIndex、RAGFlow、Dify、FastGPT
- **开发接口**：Python / Go / TypeScript SDK、CLI、REST API、Docker
- **国产芯片**：昇腾、寒武纪、燧原、壁仞、摩尔线程、昆仑芯等 10+

## 安装与使用

```bash
# 安装
pip install uv
uv pip install -U "mineru[all]"

# GPU 解析
mineru -p <input_path> -o <output_path>

# 纯 CPU 解析
mineru -p <input_path> -o <output_path> -b pipeline
```

支持 CLI、API、WebUI、mineru-router 多种使用方式，也提供在线版本（mineru.net、HuggingFace Space、ModelScope）。

## 亮点 / 个人评价

MinerU 是目前开源文档解析领域最完整、最活跃的项目之一。相比其他 PDF 解析工具，它的优势在于：(1) 从 InternLM 预训练实战中打磨出来的质量；(2) VLM + OCR 双引擎设计兼顾精度和资源消耗；(3) 全格式原生解析（不依赖转 PDF 中间步骤，DOCX 解析速度提升数十倍）；(4) 完善的 RAG 框架集成和 MCP Server 支持。3.1.0 版本从 AGPLv3 切换到 Apache 2.0 基础协议，降低了商用门槛。对于构建知识库、RAG 系统、文档智能处理流程来说，是一个非常值得采用的工具。
