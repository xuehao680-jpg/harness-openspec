## Context

Hero Section 已完成，站点有了首屏展示。现在需要全局导航栏，让用户可以在不同内容区域间切换。导航栏将固定在页面顶部，覆盖在 Hero Section 之上。

当前体系：
- 已有 `useTheme` hook（`src/hooks/useTheme.ts`）管理亮/暗模式
- 已有 CSS 变量体系（`src/index.css`）定义主题色
- Hero Section 的 CTA 已使用 `#projects` 锚点

## Goals / Non-Goals

**Goals:**
- 固定顶部导航栏，z-index 高于页面内容
- 左侧展示站点名称，右侧展示导航链接
- 链接点击平滑滚动到对应 section
- 背景模糊效果（backdrop-filter: blur）
- 响应亮/暗模式切换

**Non-Goals:**
- 不做搜索功能
- 不做多级下拉菜单
- 不做用户登录/注册
- 不包含 active link 高亮（未来可加）
- 不做移动端 hamburger 菜单（视口过窄时链接自动换行或溢出滚动）

## Decisions

### 1. 固定定位与层级

`fixed top-0 inset-x-0 z-50` — 固定在视口顶部，z-index 高于 HeroSection 的内容层（z-10）。

### 2. 布局方案

Flexbox 左右布局：`flex justify-between items-center`。
- 左侧：站点名称（`<span>` 或 `<Link>` 风格）
- 右侧：导航链接列表（`<ul>` / `<li>` / `<a>` 结构，语义化）

窄屏下导航链接允许溢出滚动（`overflow-x-auto`）或换行，不做折叠菜单。

### 3. 背景模糊

使用 CSS `backdrop-filter: blur(12px)` + 半透明背景色：

- 背景色使用 `rgba()` 形式的 CSS 变量，在亮/暗模式下拥有不同透明度
- 亮色模式：半透明白色背景（`rgba(255, 255, 255, 0.7)`）
- 暗色模式：半透明深色背景（`rgba(10, 10, 46, 0.7)`）
- `backdrop-blur-md` 提供毛玻璃效果

Tailwind CSS v4 原生支持 `backdrop-blur-*` 和 `bg-white/70` 等透明度写法。

### 4. 平滑滚动

复用 HeroSection CTA 的相同模式：`document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' })`。

Section 映射：
| 导航项 | 目标 ID | 状态 |
|--------|---------|------|
| 首页 | `#home` | 对应 HeroSection（已有） |
| 项目 | `#projects` | 已在 Hero CTA 中使用（待建） |
| 联系我 | `#contact` | 待建 |

Section 不存在时不做滚动、不抛异常。

### 5. 主题适配

导航栏半透明背景色和文字颜色通过 CSS 变量控制：
- `--nav-bg`：导航栏背景色（含透明度）
- `--nav-text`：导航栏文字色

在 `:root` 和 `.dark` 中分别定义，与已有主题体系保持一致。

## Risks / Trade-offs

| 风险 | 缓解措施 |
|------|----------|
| 导航栏遮挡 Hero 顶部内容 | 导航栏高度 ~64px，HeroSection 可通过 `scroll-mt-16` 在滚动定位时补偿 |
| backdrop-filter 兼容性（老旧浏览器） | 降级为纯半透明背景（`bg-opacity-90`），模糊为非必须体验 |
| Section 不存在时点击无反馈 | 可接受，与 Hero CTA 行为一致 |
