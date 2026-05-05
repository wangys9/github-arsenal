# Public APIs

- **地址**：https://github.com/public-apis/public-apis
- **维护方**：APILayer + 社区
- **协议**：MIT
- **分类**：开发者工具

## 简介

最全面的免费公共 API 列表，由社区维护。收录各领域的公开 API，涵盖动物、金融、天气、机器学习、政府数据等 51 个分类，每个 API 标注是否需要认证、是否支持 HTTPS、是否有 CORS 支持等信息。是开发者寻找项目所需 API 的第一站。

## 收录规模

51 个分类，1400+ 个 API。

## 主要分类

| 领域 | 典型 API |
|------|----------|
| 动物 | Cat Facts、Dog API、Shibe.Online |
| 金融 | Alpha Vantage、IEX Cloud、Plaid |
| 天气 | OpenWeatherMap、Weatherstack |
| 机器学习 | Clarifai、Dialogflow、Hugging Face |
| 地理编码 | Google Maps、HERE Maps、Mapbox |
| 政府 | Census、Data.gov、EPA |
| 健康 | CMS、NHS、OpenFDA |
| 新闻 | GNews、NewsAPI、Currents API |
| 科学与数学 | NASA、Wolfram Alpha、arXiv |
| 社交 | Discord、Reddit、TikTok |
| 运动与健身 | API-Football、Strava |
| 交通 | Amtrak、Transport for London |
| 视频 | YouTube、TMDb、Twitch |

## API 信息标注

每个 API 条目包含：

| 字段 | 说明 |
|------|------|
| Name | API 名称和链接 |
| Description | 一句话描述 |
| Auth | 认证方式（None / API Key / OAuth） |
| HTTPS | 是否支持 HTTPS |
| CORS | 跨域支持情况（Yes / No / Unknown） |

## 特色

- 按认证需求筛选（免认证 API 一目了然）
- HTTPS 和 CORS 标注帮助前端开发者快速判断可用性
- 社区持续维护，PR 审核机制保证质量
- 配套 [API 搜索工具](https://github.com/davemachado/public-api)可程序化查询

## 使用方式

直接浏览 GitHub README 按分类查找，或使用配套 API 搜索工具按关键词查询。

## 亮点 / 个人评价

开发者找 API 的"黄页"。51 个分类几乎覆盖了所有常见需求，每个 API 的认证/HTTPS/CORS 标注非常实用——前端开发者可以快速过滤出支持 CORS 的免认证 API。项目自 2016 年起持续维护，社区贡献活跃。无论你在做什么项目，大概率能在这里找到可用的免费 API。与 awesome-selfhosted 类似，是开发者工具箱中的必备参考。
