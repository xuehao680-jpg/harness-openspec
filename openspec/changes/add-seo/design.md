## Context

个人品牌站内容已就位（Hero、导航、项目、关于我），但缺少搜索引擎和社交平台所需的元数据。当前 `index.html` 只有基础 meta 标签，title 为"Qiu - Personal Website"需更新。无 `robots.txt`，无 OG/Twitter Card 标签。

## Goals / Non-Goals

**Goals:**
- 更新 title 为中文名"薛浩 - 个人主页"
- 添加 `<meta name="description">`，提炼站点描述
- 添加 Open Graph 标签（og:title, og:description, og:image, og:type, og:url）
- 添加 Twitter Card 标签（twitter:card, twitter:title, twitter:description）
- 添加 `<meta name="keywords">`
- 创建 `public/robots.txt` 允许 Google 爬虫全站索引
- 审查现有组件的语义化 HTML 使用

**Non-Goals:**
- 不做 JSON-LD 结构化数据（后续可加）
- 不做 sitemap.xml（GitHub Pages 小站暂不需要）
- 不做 Google Analytics 或其他分析工具
- 不做 canonical URL（SPA 单页应用不影响）

## Decisions

### 1. Meta 标签策略

直接在 `index.html` 的 `<head>` 中硬编码，因为是单页应用，全站共用一套 meta。

```html
<title>薛浩 - AI 数据分析师 | 个人主页</title>
<meta name="description" content="薛浩的个人主页 - AI 数据分析师，用代码将复杂的想法变成优雅的产品。" />
<meta name="keywords" content="薛浩, AI数据分析, 个人品牌, 数据科学" />
```

### 2. Open Graph 标签

在 `index.html` 中添加：

```html
<meta property="og:title" content="薛浩 - AI 数据分析师 | 个人主页" />
<meta property="og:description" content="薛浩的个人主页 - AI 数据分析师，用代码将复杂的想法变成优雅的产品。" />
<meta property="og:type" content="website" />
<meta property="og:url" content="https://qiuqiuqiu.github.io/my-website/" />
<meta property="og:image" content="https://qiuqiuqiu.github.io/my-website/og-image.png" />
```

OG image 使用站点截图或头像，先用 avatar.jpg（后续可替换为专门设计的 OG 图）。

### 3. Twitter Card

```html
<meta name="twitter:card" content="summary_large_image" />
<meta name="twitter:title" content="薛浩 - AI 数据分析师 | 个人主页" />
<meta name="twitter:description" content="薛浩的个人主页 - AI 数据分析师" />
```

### 4. robots.txt

放在 `public/` 目录，Vite 构建时自动复制到 `dist/`：

```txt
User-agent: *
Allow: /

Sitemap: https://qiuqiuqiu.github.io/my-website/sitemap.xml
```

### 5. 语义化 HTML 审查

审查现有组件并修复发现的问题：

| 组件 | 当前结构 | 结论 |
|------|---------|------|
| Navbar | `<nav>` + `<ul>`/`<li>`/`<button>` | ✅ 良好，符合语义 |
| HeroSection | `<section id="home">` + `<h1>` | ✅ 良好 |
| ProjectSection | `<section id="projects">` + `<h2>` + `<div>` 网格 | ✅ 良好 |
| 导航链接 | `<button>` 用于滚动 | ⚠️ 按钮优于 `<a href="#id">`（阻止默认跳转），但语义上链接更优。当前可接受 |

## Risks / Trade-offs

| 风险 | 缓解措施 |
|------|----------|
| OG image 不存在 | 用 avatar.jpg 替代，后续设计专用 OG 图 |
| 部署后 Google 抓取延迟 | robots.txt 和 meta 标签立即可生效，索引排队取决于 Google |
| SPA 的 SEO 局限性 | 纯客户端渲染，meta 标签对标题/描述有效，但内容爬取受限。如需深度 SEO 可考虑 SSR/SSG |
