## Why

Hero Section 已经就位，但用户缺少在页面不同区域间导航的能力。固定导航栏提供全局定位，让用户随时了解当前位置并快速跳转到目标区域，提升站点可用性和专业感。

## What Changes

- 创建 Navbar 组件，固定在视口顶部
- 左侧显示站点名称（与 Hero 姓名保持一致）
- 右侧导航链接：首页、项目、联系我
- 点击链接平滑滚动到对应 section（`#home`、`#projects`、`#contact`）
- 导航栏添加背景模糊效果（backdrop-filter: blur）
- 导航栏背景色根据亮/暗模式自适应
- 在 App.tsx 中集成 Navbar，位于 HeroSection 上方

## Capabilities

### New Capabilities
- `navigation`: 固定顶部导航栏，包含站点标识、页面导航链接、滚动定位和背景模糊效果

### Modified Capabilities

无。导航栏是新增功能，不影响已有 hero-section 的行为。

## Impact

- 新增文件：`src/components/Navbar.tsx`
- 修改文件：`src/App.tsx`（添加 Navbar）、`src/index.css`（如需要新增 CSS 变量）
- 无新增依赖
- 无 API 变更
