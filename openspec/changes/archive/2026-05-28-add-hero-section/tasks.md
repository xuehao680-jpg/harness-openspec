## 1. Cleanup & Setup

- [x] 1.1 删除 `src/App.css`，清理 `src/App.tsx` 中的默认样板代码（React logo、计数器、文档/社交链接）
- [x] 1.2 配置 Tailwind dark mode 为 `class` 策略，确保 Tailwind CSS v4 正常工作
- [x] 1.3 创建组件目录结构：`src/components/`、`src/hooks/`

## 2. 主题系统

- [x] 2.1 在 `src/index.css` 中定义亮/暗模式的 CSS 变量（背景渐变色、文字色、粒子色）
- [x] 2.2 实现 `useTheme` hook：读取系统偏好、手动切换、持久化到 localStorage
- [x] 2.3 在 `src/main.tsx` 或 `App.tsx` 中应用主题（`document.documentElement.classList` 控制 `.dark`）

## 3. Canvas 粒子背景

- [x] 3.1 实现 `BackgroundCanvas` 组件：Canvas 全屏覆盖、粒子数据生成算法
- [x] 3.2 处理窗口 resize（200ms debounce）及 Canvas 尺寸自适应
- [x] 3.3 实现主题切换时 Canvas 粒子重绘逻辑，读取 CSS 变量获取颜色
- [x] 3.4 处理 Canvas 不支持时的退化方案（纯 CSS 渐变背景）

## 4. Hero 内容区

- [x] 4.1 实现 `HeroSection` 组件：全屏高度（100dvh + fallback）、flex 居中布局
- [x] 4.2 实现身份信息展示：姓名/职业/一句话介绍，使用 Tailwind 响应式字号
- [x] 4.3 实现 CTA 按钮：样式、`scrollIntoView` 跳转到 `#projects`

## 5. 集成与验证

- [x] 5.1 在 `App.tsx` 中组装 HeroSection，包裹 BackgroundCanvas，传入个人身份数据
- [x] 5.2 验证亮/暗模式切换、Canvas 重绘、CTA 滚动行为
- [x] 5.3 真实设备测试：移动端 Safari 全屏高度、不同屏幕尺寸下的粒子密度
