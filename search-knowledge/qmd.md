# QMD — 本地文档搜索引擎

- **地址**：https://github.com/tobi/qmd
- **作者**：Tobi Lütke（Shopify 创始人）
- **协议**：MIT
- **分类**：搜索与知识管理

## 简介

QMD（Query Markup Documents）是一个完全本地运行的混合搜索引擎，专门用于搜索 Markdown 笔记、会议记录、文档和知识库。结合了 BM25 全文搜索、向量语义搜索和 LLM 重排序，所有模型通过 node-llama-cpp 本地加载，无需联网。

## 搜索方式

| 命令 | 方式 | 说明 |
|------|------|------|
| `qmd search` | BM25 全文搜索 | 快速关键词匹配 |
| `qmd vsearch` | 向量语义搜索 | 理解语义相似度 |
| `qmd query` | 混合搜索 + 重排序 | 最优质量，三者结合 |

## 搜索流程

1. 用户输入查询 → LLM 扩展查询（生成变体）
2. 对每个查询并行执行 BM25 + 向量搜索
3. RRF（倒数排名融合）合并结果，原始查询权重 ×2
4. LLM 重排序（使用 Qwen3-Reranker）
5. 位置感知混合打分，输出最终结果

## 技术亮点

- **完全本地运行**：通过 node-llama-cpp 加载 GGUF 模型，无需联网
- **三个本地模型**：embedding 模型（~300MB）、重排序模型（~640MB）、查询扩展模型（~1.1GB）
- **智能分块**：识别 Markdown 标题层级、代码块边界等自然断点来切分文档
- **AST 感知分块**：对代码文件用 tree-sitter 解析，按函数/类/接口边界切分
- **上下文系统**：给目录添加描述性元数据，帮助搜索时更好理解内容
- **MCP 服务器**：暴露 query、get、multi_get、status 工具，可直接集成到 Claude Code 等 Agent 中

## 安装

```bash
npm install -g @tobilu/qmd
# 或
bun install -g @tobilu/qmd
```
