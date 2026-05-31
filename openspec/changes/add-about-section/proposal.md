## Why

项目展示区让访客了解了技术水平，但缺少"你是谁"的个人化内容。"关于我"区域建立人格化连接，让访客了解背景和个性，增强信任感。

## What Changes

- 在项目展示区下方创建"关于我"区域（`#about`）
- 左侧展示个人照片（圆形裁剪）
- 右侧展示三段式个人简介文本
- 下方标注学校品牌标签：浙江财经大学
- 将照片从桌面复制到项目 `public/` 或 `src/assets/` 目录
- Navbar 新增"关于"导航链接

## Capabilities

### New Capabilities
- `about-section`: 个人介绍区域，包含头像照片、三段式简介和学校品牌标签

### Modified Capabilities
- `navigation`: 增加"关于"导航链接，指向 `#about`

## Impact

- 新增文件：`src/components/AboutSection.tsx`
- 复制文件：`src/assets/avatar.jpg`（从桌面获取照片）
- 修改文件：`src/App.tsx`（添加 AboutSection）、`src/components/Navbar.tsx`（新增"关于"链接）
- 无新增外部依赖
