## Why

Hero Section 展示了个人身份，访问者接下来最想了解的是"这个人做过什么项目"。项目展示区用卡片形式直观呈现作品，增强可信度和说服力。

## What Changes

- 在 Hero Section 下方创建项目展示区（`#projects`）
- 卡片式布局，每张卡片包含：项目截图、项目名称、项目简介、GitHub 链接
- 最少展示 4 个项目卡片
- 鼠标悬浮时卡片有微特效（上浮 + 阴影变化）
- Hero Section 的 CTA 按钮锚点改为跳转到这个新的项目展示区
- Navbar 的"项目"链接同样定位到此区域

## Capabilities

### New Capabilities
- `project-section`: 项目作品展示区，以卡片网格形式展示个人项目，每张卡片包含截图、名称、简介和 GitHub 链接

### Modified Capabilities
- `hero-section`: CTA 按钮的行为从"如果 #projects 不存在则无操作"变为"确实滚动到 #projects 项目展示区"，"不存在"的边界场景不再需要（因为 #projects 一定会被渲染）

## Impact

- 新增文件：`src/components/ProjectSection.tsx`、`src/components/ProjectCard.tsx`
- 修改文件：`src/App.tsx`（添加 ProjectSection 位于 HeroSection 下方）
- 无新增外部依赖
- 无 API 变更
