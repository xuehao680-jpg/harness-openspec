## Context

个人品牌站目前有 Hero Section 和导航栏，但缺少展示作品的核心内容区。项目展示区将填补这一空白，让访客直观了解开发者的项目经验。

已有能力：
- Hero Section（带 `#home` 锚点）和导航栏（含"项目"链接到 `#projects`）
- 完整的主题系统（CSS 变量 + useLayoutEffect 同步）
- Tailwind CSS v4 网格和动画工具类

## Goals / Non-Goals

**Goals:**
- 在 Hero Section 下方创建项目展示区，添加 `#projects` 锚点
- 卡片网格布局，响应式列数
- 每张卡片：项目截图、名称、简介、GitHub 链接
- 悬浮微特效（上浮 + 阴影加深）
- 所有图片使用 lazy loading

**Non-Goals:**
- 不做项目详情页
- 不做项目搜索
- 不做分页或加载更多
- 不做筛选/分类

## Decisions

### 1. 布局方案

Tailwind Grid 响应式布局：
- 移动端：1 列
- 平板：2 列
- 桌面：3 列（`grid-cols-1 md:grid-cols-2 lg:grid-cols-3`）
- 居中对齐，最大宽度限制（`max-w-6xl mx-auto`）

4 个项目以上时自动换行，无需额外处理。

### 2. 卡片设计

卡片结构（从上到下）：
```
┌──────────────────┐
│  项目截图 (16:9)  │
├──────────────────┤
│  项目名称         │
│  项目简介         │
│  [GitHub 链接]    │
└──────────────────┘
```

- 截图区域用 `<div>` 包裹 `<img>`，固定宽高比 `aspect-video`，对象适应 `object-cover`
- 名称使用 `text-xl font-semibold`
- 简介使用 `text-sm` 或 `text-base`
- GitHub 链接用 SVG 图标 + 文字，新标签打开

### 3. 悬浮微特效

使用 Tailwind 过渡类：
- `transition-all duration-300 ease-out` — 平滑过渡
- `hover:-translate-y-2` — 卡片上浮 8px
- `hover:shadow-xl` — 阴影加深
- 可选的 `hover:border-*` 或 `hover:ring-*` 边框高亮

尊重 `prefers-reduced-motion`：通过 `motion-safe:` 前缀仅在用户未开启减少动效时应用 hover 动画。

### 4. 项目数据

直接以数组形式定义，导出为常量，放在 `src/data/projects.ts` 中便于后续维护。每条数据包含：
```ts
interface Project {
  title: string
  description: string
  image: string
  github: string
}
```

截图先用占位图（`https://placehold.co/`），后续替换为真实截图。

### 5. 主题适配

卡片背景色、文字色、阴影颜色通过 CSS 变量或 Tailwind 的 `dark:` 前缀控制：
- 亮色：`bg-white` + `shadow-md`
- 暗色：`dark:bg-gray-800` + `dark:shadow-gray-900/30`

### 6. CTA 锚点更新

Hero Section 的 CTA 按钮已经使用 `#projects`，ProjectSection 渲染时自带 `id="projects"`，CTA 自然生效。"不存在"的边界场景不再发生。

## Risks / Trade-offs

| 风险 | 缓解措施 |
|------|----------|
| 项目截图尚未就绪（占位图） | 使用占位图服务，后续一键替换为真实图片链接 |
| 卡片数量不足 4 个 | 先用占位项目填充到至少 4 个，后续替换内容和截图 |
| prefers-reduced-motion | hover 动效使用 `motion-safe:` 前缀控制 |
| 图片加载影响 LCP | 使用 lazy loading + 宽高比预留空间防止 CLS |
