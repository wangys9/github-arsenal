# GraphRAG

- **地址**：https://github.com/microsoft/graphrag
- **文档**：https://microsoft.github.io/graphrag
- **论文**：https://arxiv.org/pdf/2404.16130
- **作者**：Microsoft Research
- **协议**：MIT
- **分类**：大模型工具

## 简介

微软研究院开源的 GraphRAG 项目，是一个数据管道和转换套件，利用 LLM 从非结构化文本中提取有意义的结构化数据，构建知识图谱记忆结构来增强 LLM 输出质量。核心目标是让 LLM 更好地推理用户的私有数据。

## 核心机制

传统 RAG 基于向量相似度检索文档片段，适合局部查询但无法回答需要跨文档综合推理的问题。GraphRAG 通过以下方式解决：

1. **索引阶段**：LLM 对原始文本进行实体抽取和关系构建，生成知识图谱 + 社区层级结构
2. **查询阶段**：利用图结构和社区摘要进行全局查询（Global Search）和局部查询（Local Search），支持跨文档的主题聚合和推理

## 两种查询模式

| 模式 | 适用场景 | 工作方式 |
|------|---------|---------|
| **Global Search** | 需要跨文档综合理解的主题性问题 | 利用社区摘要自底向上聚合答案 |
| **Local Search** | 针对特定实体的细节性问题 | 从实体出发遍历关联子图 |

## 安装使用

```bash
pip install graphrag
graphrag init --root ./myproject
graphrag index --root ./myproject
graphrag query --root ./myproject --method global "主题摘要问题"
```

## 注意事项

- **索引成本较高**：GraphRAG 的索引过程需要大量 LLM 调用，建议从小数据集开始
- **Prompt 调优**：开箱即用的效果可能不理想，强烈建议按照文档的 Prompt Tuning Guide 进行调优
- **版本升级**：小版本升级需运行 `graphrag init --root [path] --force` 更新配置格式

## 技术栈

- Python
- LLM 驱动的实体/关系抽取
- 知识图谱 + 社区检测（Leiden 算法）
- 支持多种 LLM 后端（OpenAI、Azure OpenAI 等）

## 亮点 / 个人评价

GraphRAG 解决了传统 RAG 无法跨文档推理的核心痛点。对于需要理解大量叙事性私有数据（如企业文档、研究报告）并回答综合性问题的场景，知识图谱 + 社区摘要的方案比纯向量检索更有效。代价是索引成本较高，适合对回答质量有要求、能接受前期投入的场景。微软研究院的背书和活跃的社区讨论使其成为 RAG 领域的重要参考实现。
