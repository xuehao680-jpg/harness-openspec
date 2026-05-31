## Why

个人品牌站需要一个引人注目的首屏来建立第一印象。当前页面是 Vite 默认模板，没有任何个人品牌信息。Hero Section 是访客进入网站首先看到的内容，直接决定了用户是否愿意继续浏览。

## What Changes

- 创建 HeroSection 组件，包含：
  - 全屏高度（100dvh）的展示区域
  - 居中显示：名字、职业/头衔、一句话个人介绍
  - CTA 按钮，点击后平滑滚动到项目区域
- 背景系统：CSS 渐变色底层 + Canvas 绘制的静态粒子叠加层
- 支持明亮/暗黑模式自适应（跟随系统或手动切换）
- 移除 Vite 默认模板的样板内容（React logo、计数器、文档/社交链接等）

## Capabilities

### New Capabilities
- `hero-section`: 网站首屏 Hero 区域，包含个人身份展示、CTA 引导和科技感粒子渐变背景

### Modified Capabilities

无。当前项目尚无已有 spec。

## Impact

- 新增文件：`src/components/HeroSection.tsx`、`src/components/BackgroundCanvas.tsx`、`src/hooks/useTheme.ts`
- 修改文件：`src/App.tsx`（用 HeroSection 替换默认内容）、`src/index.css`（全局主题变量）
- 删除文件：`src/App.css`（默认样式将被 Tailwind 替代）
- 无新增依赖
- 无 API 变更
