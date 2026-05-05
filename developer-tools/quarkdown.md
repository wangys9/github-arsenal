# Quarkdown

- **地址**：https://github.com/iamgio/quarkdown
- **官网**：https://quarkdown.com
- **协议**：GPLv3（CLI 和 LSP 模块为 AGPLv3）
- **分类**：开发者工具

## 简介

一个基于 Markdown 的现代排版系统，通过引入函数、变量等图灵完备的语法扩展，让同一个项目无缝编译为学术论文、书籍、演示文稿、静态网站或知识库。核心思路是用 Markdown 的简洁语法替代 LaTeX 的复杂命令，同时保持同等程度的排版控制力。

## 核心特性

- **函数调用**：在 Markdown 中直接调用函数，支持参数和函数体
- **自定义函数与变量**：在 Markdown 源码中定义函数和变量
- **标准库**：内置布局构建器、I/O、数学运算、条件语句、循环等
- **多目标输出**：同一源码编译为不同格式
- **VS Code 扩展**：语法高亮、实时预览、自动补全
- **项目向导**：`quarkdown create` 交互式创建项目
- **REPL 模式**：交互式实验语言特性

## 输出目标

| 目标 | 说明 | 底层技术 |
|------|------|----------|
| Plain HTML | 连续流式页面（类 Notion/Obsidian） | — |
| Paged HTML | 论文、文章、书籍 | paged.js |
| Slides | 交互式演示文稿 | reveal.js |
| Docs | Wiki、技术文档、知识库 | — |
| PDF | 所有 HTML 类型均支持导出 | Puppeteer |
| Plain Text | 纯文本输出 | — |

通过 `.doctype {plain|paged|slides|docs}` 函数切换输出类型。

## 与其他工具对比

| 特性 | Quarkdown | LaTeX | Typst | AsciiDoc | MDX |
|------|:---------:|:-----:|:-----:|:--------:|:---:|
| 简洁可读 | ✅ | ❌ | ✅ | ✅ | ✅ |
| 完整文档控制 | ✅ | ✅ | ✅ | ❌ | ❌ |
| 脚本能力 | ✅ | 部分 | ✅ | ❌ | ✅ |
| 书籍/文章导出 | ✅ | ✅ | ✅ | ✅ | 第三方 |
| 演示文稿导出 | ✅ | ✅ | ✅ | ✅ | 第三方 |
| 学习曲线 | 低 | 高 | 中 | 低 | 低 |

## 语法示例

```markdown
.tableofcontents

# Section

## Subsection

1. **First** item
2. **Second** item

.center
    This text is _centered_.

.row alignment:{spacebetween}
    ![Image 1](img1.png)
    ![Image 2](img2.png)
    ![Image 3](img3.png)
```

等价 LaTeX 需要 `\begin{enumerate}`、`\begin{center}`、`\begin{figure}` 等大量样板代码。

## 安装

```bash
# Linux/macOS
curl -fsSL https://raw.githubusercontent.com/quarkdown-labs/get-quarkdown/main/install.sh | sudo bash

# Homebrew
brew install quarkdown-labs/quarkdown/quarkdown

# Windows (PowerShell)
irm https://raw.githubusercontent.com/quarkdown-labs/get-quarkdown/main/install.ps1 | iex
```

需要 Java 17+，PDF 导出需要 Node.js + Puppeteer。

## 编译

```bash
quarkdown c file.qd              # 编译
quarkdown c file.qd -p -w        # 实时预览（监听文件变化自动重编译）
quarkdown c file.qd --pdf        # 导出 PDF
quarkdown repl                   # 交互式 REPL
```

## 亮点 / 个人评价

用图灵完备的函数扩展把 Markdown 从"格式化文本"提升到"排版系统"的高度。对比 LaTeX，语法简洁度提升巨大，学习曲线极低。多目标输出（论文/幻灯片/网站/文档）这个能力非常独特——一套源码覆盖所有场景。VS Code 实时预览体验流畅，项目向导降低了上手门槛。对于需要写学术论文但不想学 LaTeX 的用户，或者想用 Markdown 同时产出文档和演示的开发者，Quarkdown 是一个值得关注的新选择。
