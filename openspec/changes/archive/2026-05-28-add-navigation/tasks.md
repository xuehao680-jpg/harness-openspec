## 1. 导航栏组件

- [x] 1.1 在 `src/index.css` 中添加导航栏 CSS 变量（`--nav-bg`、`--nav-text`），亮/暗各一套
- [x] 1.2 创建 `Navbar` 组件：`fixed top-0 inset-x-0 z-50`、flex 布局（左名称、右链接）
- [x] 1.3 实现导航链接点击平滑滚动逻辑：`getElementById` + `scrollIntoView({ behavior: 'smooth' })`，处理目标不存在的情况
- [x] 1.4 添加背景模糊效果：`backdrop-blur-md` + 半透明背景色，兼容不支持 `backdrop-filter` 的浏览器

## 2. 集成与验证

- [x] 2.1 在 `App.tsx` 中添加 Navbar，给 HeroSection 添加 `id="home"` 锚点
- [x] 2.2 验证导航链接点击滚动、背景模糊效果、亮/暗模式切换
