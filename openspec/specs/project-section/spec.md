## ADDED Requirements

### Requirement: 项目展示区布局

项目展示区位于 Hero Section 下方，使用响应式卡片网格布局。

- Section 使用 `id="projects"` 作为锚点
- 移动端 1 列，平板 2 列，桌面 3 列
- 内容居中，最大宽度有限制

#### Scenario: 项目展示区显示在 Hero 下方

- **GIVEN** 用户访问网站首页
- **WHEN** 页面加载完成
- **THEN** 项目展示区位于 Hero Section 下方
- **AND** 展示区带有 `#projects` 锚点

#### Scenario: 响应式列数变化

- **GIVEN** 项目展示区已加载
- **WHEN** 视口宽度从桌面变为移动端
- **THEN** 卡片网格从 3 列变为 1 列

---

### Requirement: 项目卡片内容

每张项目卡片展示一个项目的完整信息。

- 项目截图：宽高比 16:9，使用 `object-cover` 适配
- 项目名称：使用较大字号
- 项目简介：简要描述项目
- GitHub 链接：在新标签页打开

#### Scenario: 正常展示项目卡片

- **GIVEN** 项目展示区已加载
- **WHEN** 用户查看项目卡片
- **THEN** 卡片包含截图、名称、简介和 GitHub 链接
- **AND** 截图使用 lazy loading 加载

#### Scenario: 截图加载失败

- **GIVEN** 项目卡片的截图 URL 无效
- **WHEN** 图片加载失败
- **THEN** 显示占位背景色，不影响卡片布局
- **AND** 其余内容（名称、简介、链接）正常显示

---

### Requirement: 最少 4 个项目

项目展示区至少展示 4 个项目，不足时用占位项目填充。

#### Scenario: 展示 4 个项目

- **GIVEN** 项目数据包含 4 个项目
- **WHEN** 页面加载
- **THEN** 展示区显示 4 张项目卡片
- **AND** 所有卡片布局一致，对齐整齐

---

### Requirement: 悬浮微特效

鼠标悬浮在卡片上时触发微特效。

- 卡片上浮（`translateY(-8px)`）
- 阴影加深
- 过渡动画使用 `duration-300`
- 尊重 `prefers-reduced-motion`

#### Scenario: 鼠标悬浮卡片

- **GIVEN** 项目展示区已加载
- **WHEN** 用户将鼠标悬浮在一张卡片上
- **THEN** 卡片向上浮动
- **AND** 卡片阴影加深
- **AND** 过渡平滑

#### Scenario: 用户开启减少动效

- **GIVEN** 用户在系统设置中开启了"减少动效"
- **WHEN** 用户将鼠标悬浮在卡片上
- **THEN** 卡片不产生上浮和阴影动画
