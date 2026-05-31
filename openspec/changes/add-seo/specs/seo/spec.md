## ADDED Requirements

### Requirement: HTML Meta 标签

页面 `<head>` 中包含完整的 SEO meta 标签。

- `<title>` 使用中文名
- `<meta name="description">` 提供站点描述
- `<meta name="keywords">` 提供关键词

#### Scenario: 搜索引擎读取 meta

- **GIVEN** Google 爬虫访问网站首页
- **WHEN** 爬虫解析 HTML
- **THEN** `<title>` 包含"薛浩 - AI 数据分析师 | 个人主页"
- **AND** `<meta name="description">` 包含站点描述内容

---

### Requirement: Open Graph 标签

页面包含社交媒体分享所需的 OG 标签。

- 包含 `og:title`、`og:description`、`og:type`、`og:url`、`og:image`

#### Scenario: 社交媒体分享

- **GIVEN** 用户将网站链接分享到微信或 Slack
- **WHEN** 社交平台抓取页面
- **THEN** 展示标题、描述和预览图片

---

### Requirement: Twitter Card 标签

页面包含 Twitter 卡片所需的标签。

- 包含 `twitter:card`、`twitter:title`、`twitter:description`

#### Scenario: Twitter 分享

- **GIVEN** 用户将网站链接分享到 Twitter
- **WHEN** Twitter 抓取页面
- **THEN** 展示 Large Summary Card 样式

---

### Requirement: robots.txt

网站根目录可访问 `robots.txt`，允许 Google 爬虫索引。

- 允许所有爬虫抓取全站内容
- 文件放置在 `public/` 目录

#### Scenario: 爬虫访问 robots.txt

- **GIVEN** Google 爬虫准备抓取网站
- **WHEN** 访问 `/robots.txt`
- **THEN** 返回允许全站抓取的规则
- **AND** HTTP 状态码为 200

---

### Requirement: 语义化 HTML

网站组件使用标准的语义化 HTML 元素。

- 导航使用 `<nav>`
- 列表使用 `<ul>` / `<ol>`
- 内容分区使用 `<section>`
- 主标题使用 `<h1>`，分区标题使用 `<h2>`

#### Scenario: 无障碍工具识别结构

- **GIVEN** 用户使用屏幕阅读器访问网站
- **WHEN** 屏幕阅读器解析页面结构
- **THEN** 能够识别导航区、主内容区、项目区等语义区块
