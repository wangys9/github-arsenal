# Reddit Toolkit

- **地址**：https://github.com/YoriHan/Reddit-
- **作者**：YoriHan
- **协议**：MIT
- **分类**：开发者工具

## 简介

专为独立开发者和出海营销人设计的 Reddit CLI 工具。核心思路：先深度理解一个社区（写作风格、规则禁忌），再生成真正融入那里的内容，而不是盲目发帖被当成广告删除。基于 Anthropic Claude API 驱动全部 AI 功能，集成 Notion 进行内容管理。

## 核心工作流

```
产品描述 → 自动发现匹配的 Subreddits → 学习社区风格和规则 → 生成仿风格帖子 → 推送 Notion
```

一条命令完成全流程：

```bash
reddit-toolkit pipeline run --product myapp
```

## 核心特性

- **产品档案**：支持文字描述、代码仓库、网页链接三种方式创建产品画像，AI 自动理解产品定位
- **Subreddit 匹配**：AI 搜索并评估适合产品的社区，输出订阅人数、自我推广容忍度、建议切入角度
- **深度社区学习**：
  - **风格学习**（`style learn`）：抓取热门帖子，建立写作风格档案（语气、标题套路、表达习惯）
  - **规则学习**（`rules learn`）：分析官方规则 + AI 推断隐性规范（什么内容会被删、安全发帖角度）
- **仿风格写作**（`style mimic`）：生成的帖子读起来像社区老用户写的，自动注入规则约束，自动去 AI 味
- **机会扫描**：监控 subreddit，找出有人在问你产品能解决的问题，AI 评分 + 生成回复草稿
- **自动 Pipeline**：`pipeline daemon` 定时运行，发现新社区 → 学习 → 生成 → 推送 Notion，全程自动化
- **Notion 集成**：帖子草稿和规则档案分别推送到不同 Notion 数据库，方便团队协作

## 缓存与数据流

| 缓存类型 | 过期时间 | 说明 |
|----------|----------|------|
| 写作风格 | 7 天 | 帖子语气、标题套路 |
| 隐性规范 | 7 天 | AI 观察的社区氛围和禁忌 |
| 官方规则 | 30 天 | Reddit 侧边栏规则 |

本地缓存路径：`~/.reddit-toolkit/`（profiles / styles / rules / tracker / state / notion）

## 安装与使用

```bash
pip install reddit-toolkit

# 必须：设置 Anthropic API Key
export ANTHROPIC_API_KEY=sk-ant-...
```

```bash
# 创建产品档案（三种方式）
reddit-toolkit product create --name "MyApp" --description "帮开发者生成 API 文档的 CLI"
reddit-toolkit product create --name "MyApp" --from-dir ./my-project
reddit-toolkit product create --name "MyApp" --from-url https://myapp.com

# 完整 Pipeline（推荐）
reddit-toolkit pipeline run --product myapp
reddit-toolkit pipeline daemon --product myapp --interval 1d  # 每天自动运行

# 逐步操作
reddit-toolkit style learn --subreddit SideProject        # 学习社区
reddit-toolkit style mimic --subreddit SideProject \
  --product myapp --topic "产品发布"                       # 生成帖子

# 机会扫描
reddit-toolkit scan daemon --product myapp --interval 8h  # 每8小时扫描
```

## 亮点 / 个人评价

- **解决真问题**：独立开发者出海最大的痛点之一就是 Reddit 营销——不了解社区文化就发帖，轻则被无视，重则被封号。这个工具系统性地解决了这个问题
- **先理解再创作**：不是简单的 AI 写帖工具，核心是"学习社区 → 理解规则 → 再生成内容"，这个思路很对
- **规则自动注入**：生成内容时自动带入社区约束，避免踩雷，这是关键差异化能力
- **Pipeline 自动化**：从发现社区到推送 Notion 全链路自动化，适合长期运营
- **中文输出**：规则档案全部中文呈现，对中文开发者友好
- **本地缓存设计**：合理的 TTL 机制避免重复 API 调用，节省成本
