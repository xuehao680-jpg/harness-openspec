## Context

站点已有 Hero、项目展示区，现在需要"关于我"区域来建立人格化连接。该区域展示个人照片、三段式简介和学校品牌标签。

## Goals / Non-Goals

**Goals:**
- 在项目展示区下方创建"关于我"区域（`#about`）
- 桌面端左右布局：左侧照片 + 右侧文字
- 移动端上下布局：照片在上，文字在下
- 照片圆形裁剪，响应式大小
- 三段式个人简介
- 底部显示"浙江财经大学"品牌标签
- Navbar 新增"关于"链接

**Non-Goals:**
- 不做联系表单
- 不做技能标签云
- 不做时间线

## Decisions

### 1. 布局方案

桌面端：`flex flex-row items-center gap-12` — 照片在左，文字在右
移动端：通过 `flex-col md:flex-row` 切换为上下堆叠

照片容器：`w-48 h-48 md:w-64 md:h-64`，`rounded-full` 圆形裁剪

### 2. 照片处理

从用户桌面 `微信图片_20260402230840_161_100.jpg` 复制到 `src/assets/avatar.jpg`。

使用 `object-cover rounded-full` 确保图片适配圆形容器。添加 `border-4` 边框提升视觉层次。

### 3. 简介文本

三段文字，使用 `<p>` 标签 + `space-y-4` 间距：
- 第一段：自我介绍（姓名、职业背景）
- 第二段：专业领域和技能
- 第三段：个人兴趣和价值观

### 4. 品牌标签

使用 Tailwind Badge 样式：`inline-block rounded-full px-4 py-1.5 text-sm font-medium`，背景色跟随主题。

### 5. 主题适配

- 背景色使用 CSS 变量（与项目展示区一致）
- 文字色使用 `var(--text-primary)` / `var(--text-secondary)`
- 照片边框使用 `border-gray-200 dark:border-gray-600`
