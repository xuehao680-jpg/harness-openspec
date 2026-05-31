## Context

个人品牌站的首个定制功能。当前页面为 Vite 默认模板，需要替换为展示个人身份的全屏 Hero 区域。Hero Section 是首屏最关键的内容区块，直接影响访客第一印象。

设计约束：
- 项目已有 Tailwind CSS v4 + Tailwind CSS Vite 插件配置
- 尚无自定义组件、hooks 或全局主题系统
- 部署环境为 GitHub Pages，base path `/my-website/`
- 纯前端项目，无后端依赖

## Goals / Non-Goals

**Goals:**
- 全屏高度 Hero 区域，居中展示个人身份信息（名字、职业、一句话介绍）
- CSS 渐变色背景 + Canvas 静态粒子叠加的科技感视觉效果
- 支持明亮/暗黑模式切换
- CTA 按钮可跳转到项目区域
- 清理 Vite 默认模板的样板代码

**Non-Goals:**
- 不做入场动效、过渡动画、滚动动画
- 不做导航栏
- 不做后端 API 调用
- 不做路由系统
- 不做 SEO meta 标签（后续单独处理）

## Decisions

### 1. 全屏高度方案：100dvh + fallback

| 方案 | 说明 | 结论 |
|------|------|------|
| `100vh` | iOS Safari 地址栏会吃掉空间，底部被截断 | ❌ |
| `100dvh` | 动态 viewport height，Safari 15.4+ 支持 | ✅ 首选 |
| JS 计算高度 | 兼容性好但 FOUC 风险 | ⚠️ fallback |

使用 `100dvh`，不支持 `dvh` 的浏览器通过 Tailwind 的 `min-h-screen` 兜底。

### 2. 粒子绘制：Canvas 动画绘制

粒子采用 Canvas + requestAnimationFrame 驱动缓慢漂移：

- 每个粒子分配随机速度向量（0.1~0.4 px/frame），方向随机
- 粒子触边环绕，永不消失
- 粒子间连线距离随粒子运动实时更新
- 标签页隐藏时通过 visibilitychange 暂停动画，节省 CPU
- 尊重 `prefers-reduced-motion`，开启时退化为一次性静态绘制
- 主题切换时只更新颜色，不重新生成粒子位置

| 方案 | 优点 | 缺点 |
|------|------|------|
| Canvas 动画绘制 | 视觉动态感强，完全控制效果 | 需处理性能、标签页可见性 |
| CSS 伪元素 / SVG | 更简单 | 无法生成复杂粒子图案，主题切换处理麻烦 |
| 预生成图片 | 最简单 | 不响应尺寸变化，不灵活 |

选择 Canvas 延续未来扩展性，同时当前保持静态。

### 3. 主题系统：CSS 变量 + useLayoutEffect 同步

采用 Tailwind 的 `class` 策略控制暗黑模式（`@custom-variant dark (&:is(.dark *))`），配合 CSS 自定义属性驱动所有颜色：

- CSS 变量在 `:root` 和 `.dark` 下定义两套色值，包括渐变色、粒子色、文字色、CTA 色
- HeroSection 的文字和背景颜色全部通过 `style={{ color: 'var(--text-primary)' }}` 引用 CSS 变量，不使用 `dark:` 前缀（CSS 变量方案更简洁，且 Canvas 需通过 getComputedStyle 读取 ）
- Canvas 通过 `useLayoutEffect` 同步读取 CSS 变量获取当前主题色
- 主题切换使用 `useLayoutEffect` 确保 `.dark` 类添加和 Canvas 颜色更新均在 paint 前完成，避免闪烁

### 4. CTA 按钮行为

调用 `element.scrollIntoView({ behavior: 'smooth' })` 定位到项目区域。使用 `#projects` 作为锚点标识。

### 5. 个人身份数据

直接以 props 形式传入 HeroSection 组件，数据在当前阶段硬编码在 App.tsx 中，后续可抽取为配置文件。

## Risks / Trade-offs

| 风险 | 缓解措施 |
|------|----------|
| iOS Safari 100vh 截断 | 使用 `100dvh` + `min-h-screen` 双层保障 |
| 窗口 resize 导致 Canvas 频繁重绘 | 添加 debounce（200ms） |
| 主题切换 Canvas 闪烁 | 切换到新主题色后再触发重绘，避免颜色跳变 |
| Canvas 在不支持 Canvas 的浏览器（极罕见） | 退化到纯 CSS 渐变背景 |
| prefers-reduced-motion | 检测用户偏好，有动画时退化为静态绘制 |
