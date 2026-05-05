# Karpathy-Inspired Claude Code Guidelines

- **地址**：https://github.com/forrestchang/andrej-karpathy-skills
- **作者**：forrestchang ([@jiayuan_jy](https://x.com/jiayuan_jy))
- **协议**：MIT
- **分类**：开发者工具

## 简介

一个单文件 `CLAUDE.md`，从 Andrej Karpathy 对 LLM 编码陷阱的观察中提炼出四条原则，用于改善 Claude Code 的编码行为。解决 LLM 在编程中常见的盲目假设、过度工程、不相关改动和缺乏验证等问题。

## 核心原则

| 原则 | 解决的问题 |
|------|-----------|
| **先思考再编码** | 错误假设、隐藏困惑、遗漏权衡 |
| **简单至上** | 过度复杂化、臃肿抽象 |
| **精准改动** | 不相关编辑、误触不该改的代码 |
| **目标驱动执行** | 缺乏验证、模糊的成功标准 |

### 1. 先思考再编码

- 不确定时主动提问，而非默默猜测
- 存在歧义时列出多种理解
- 发现更简单方案时敢于反驳
- 遇到困惑时停下来澄清

### 2. 简单至上

- 只实现被要求的功能，不添加额外特性
- 单次使用的代码不做抽象
- 不为不可能发生的场景写错误处理
- 如果 200 行能缩到 50 行，就重写

### 3. 精准改动

- 不"顺手改进"相邻代码、注释或格式
- 不重构没坏的东西
- 匹配现有风格，即使你不会这么做
- 注意到无关死代码时提一句，但不主动删除

### 4. 目标驱动执行

将命令式指令转换为可验证的声明式目标：

| 命令式 | 转换为 |
|--------|--------|
| "添加校验" | "为无效输入写测试，然后让它们通过" |
| "修复 Bug" | "写一个复现它的测试，然后让测试通过" |
| "重构 X" | "确保重构前后测试都通过" |

## 安装方式

**方式 A：Claude Code 插件（推荐）**
```
/plugin marketplace add forrestchang/andrej-karpathy-skills
/plugin install andrej-karpathy-skills@karpathy-skills
```

**方式 B：直接使用 CLAUDE.md**
```bash
curl -o CLAUDE.md https://raw.githubusercontent.com/forrestchang/andrej-karpathy-skills/main/CLAUDE.md
```

也支持 Cursor（通过 `.cursor/rules/karpathy-guidelines.mdc`）。

## 亮点 / 个人评价

Karpathy 的洞察切中要害——LLM 最擅长的是"循环直到满足目标"，而非逐条执行指令。"目标驱动执行"原则将这一优势最大化：给 LLM 成功标准而非操作步骤，让它自主循环验证。这种思路对日常使用 Claude Code 编程有直接帮助。
