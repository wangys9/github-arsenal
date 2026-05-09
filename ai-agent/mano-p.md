# Mano-P

- **地址**：https://github.com/Mininglamp-AI/Mano-P
- **团队**：明略科技（Mininglamp AI）
- **协议**：Apache 2.0
- **论文**：[arXiv:2509.17336](https://arxiv.org/abs/2509.17336)
- **分类**：AI Agent
- **标签**：GUI Agent、端侧推理、Apple Silicon、VLA、Computer Use

## 简介

面向边缘设备的开源 GUI-VLA（Vision-Language-Action）Agent 模型。通过纯视觉理解驱动桌面 GUI 自动化操作，可在 Apple M4 芯片本地运行，无需云 API 调用，所有截图和任务数据保留在设备端。Mano = 西班牙语"手"，P = Private（私有 AI）。

## 核心特性

- **复杂 GUI 自动化**：自主完成包含数百个交互元素的复杂界面操作
- **纯视觉理解**：不依赖 HTML 解析或系统 API，支持桌面软件、Web 应用、3D 应用等所有 GUI 类型
- **端侧推理**：4B 模型可直接在 Mac mini/MacBook（M4 芯片 + 32GB RAM）上运行，72B 模型支持算力棒
- **Cider 推理加速 SDK**：基于 MLX 开发，提供 MLX 缺失的 W8A8/W4A8 激活量化，Apple M5 Pro 上实现 1.4x–2.2x prefill 加速
- **Mano-AFK 全自动应用构建**：一句话需求 → 代码生成 → 部署 → E2E 测试 → 自动修复，全程无人工干预

## Benchmark 表现

| 基准 | 指标 | 结果 |
|------|------|------|
| OSWorld（专项模型） | 成功率 | **58.2%**（#1，超第二名 13.2pp） |
| WebRetriever Protocol I | NavEval | **41.7**（超 Claude 4.5 Computer Use 的 31.3） |
| Apple M5 Pro 推理 | Decode 速度 | **~80 tokens/s**（Mano-P 1.0-4B） |
| Cider W8A8 加速 | Prefill 提速 | **~12.7%**（vs W8A16 baseline） |

## 使用方式

### 1. mano-cua（CLI 命令行工具）

面向人类用户，快速执行 GUI 自动化任务：

```bash
# 安装
brew tap Mininglamp-AI/tap && brew install mano-cua

# 云端模式（默认）
mano-cua run "打开微信告诉FTY会议延期"

# 本地模式（完全离线）
mano-cua install-sdk && mano-cula install-model
mano-cua run "打开Safari搜索Python" --local
```

### 2. mano-skill（ClawHub Skill）

面向 AI Agent（Claude Code / OpenClaw），Agent 自主调用 GUI 自动化能力：

```bash
# 通过 ClawHub CLI 安装
clawhub install mano-cua
```

### 3. Mano-AFK（全自动应用构建）

从自然语言需求到可运行应用的端到端自动化：

- GitHub: [Mininglamp-AI/mano-afk](https://github.com/Mininglamp-AI/mano-afk)
- ClawHub: [clawhub.ai/hanningwang/mano-afk](https://clawhub.ai/hanningwang/mano-afk)

## 技术架构

- **训练方法**：Mano-Action 双向自强化学习（Text↔Action 循环一致性）
- **三阶段渐进训练**：SFT → Offline RL → Online RL
- **推理闭环**：think-act-verify 循环推理机制
- **边缘优化**：混合精度量化 + 视觉 Token 剪枝（GSPruning）+ 边缘推理适配
- **模型下载**：[HuggingFace](https://huggingface.co/Mininglamp-2718/Mano-P) · [ModelScope](https://modelscope.cn/models/Mininglamp/Mano-P)

## 与竞品对比

| 维度 | Mano-P | OpenClaw | Manus | 传统 RPA |
|------|--------|----------|-------|----------|
| 模型来源 | 内置端侧模型 | 用户配置 | 云端 API | 无模型 |
| 数据安全 | 本地执行 | 部分云端 | 云端推理 | 可本地 |
| 控制方式 | 纯视觉 | CDP 协议 | HTML 解析 | 系统 API |
| 适用场景 | 全类型 GUI | 多类应用 | 仅 Web | 特定系统 |

## 亮点 / 个人评价

- **端侧 GUI Agent 的突破**：在 Apple Silicon 上实现完全本地化的 GUI 自动化，隐私性极强
- **Benchmark 领先**：OSWorld 第一名，WebRetriever 超越 Claude 4.5 Computer Use
- **生态完善**：CLI 工具 + Claude Code Skill + 全自动应用构建，覆盖不同用户场景
- **Cider SDK 通用价值**：W8A8 量化加速不仅适用于 Mano-P，任何 MLX 模型都能受益
- **明略科技出品**：国内公司在端侧 AI Agent 领域的有力探索
