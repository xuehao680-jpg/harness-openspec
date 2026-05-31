## Why

网站内容已经完善（Hero、导航、项目、关于我），但搜索引擎无法有效理解和索引这些内容。添加 SEO 基础优化和社交身份支持，让网站在 Google 搜索结果和社交媒体分享中呈现专业形象。

## What Changes

- 更新 `index.html` 的 meta 标签：`title`、`description`、`keywords`
- 添加 Open Graph（OG）标签：`og:title`、`og:description`、`og:image`、`og:url`
- 添加 Twitter Card 标签
- 添加 `robots.txt` 允许 Google 爬虫索引
- 审查现有组件的语义化 HTML，确保无障碍和 SEO 友好
- 必要时修复语义结构（如 `<main>`、`<section>`、`<nav>` 的正确使用）

## Capabilities

### New Capabilities
- `seo`: SEO 基础优化，包含 meta 标签、结构化标记、robots.txt 和社交分享支持

### Modified Capabilities

无。SEO 是新增能力，不改变现有功能的行为。

## Impact

- 新增文件：`public/robots.txt`
- 修改文件：`index.html`（新增 meta/OG/Twitter 标签）
- 审查文件：现有组件（检查语义化 HTML）
- 无新增依赖
- 无 API 变更
