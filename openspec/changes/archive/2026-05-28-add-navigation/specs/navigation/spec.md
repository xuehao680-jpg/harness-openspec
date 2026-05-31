## ADDED Requirements

### Requirement: 导航栏固定定位

导航栏固定在视口顶部，不随页面滚动而移动。

- 使用 `position: fixed`，位于 `top: 0`，左右撑满
- z-index 高于页面其他内容（包括 Hero Section）
- 导航栏在页面加载完成后立即可见

#### Scenario: 页面滚动时导航栏保持顶部

- **GIVEN** 用户访问网站
- **WHEN** 用户向下滚动页面
- **THEN** 导航栏始终固定在视口顶部

#### Scenario: 导航栏层级不被内容遮挡

- **GIVEN** 页面包含 Hero Section 和导航栏
- **WHEN** 页面渲染完成
- **THEN** 导航栏位于 Hero Section 之上，不 Hero 内容遮挡

---

### Requirement: 导航栏内容布局

导航栏左侧显示站点名称，右侧显示导航链接。

- 站点名称与 Hero 中的姓名一致
- 导航链接包含：首页、项目、联系我
- 使用 Flexbox 左右布局

#### Scenario: 正常显示导航栏内容

- **GIVEN** 导航栏已加载
- **WHEN** 用户查看页面顶部
- **THEN** 左侧显示站点名称
- **AND** 右侧依次显示"首页"、"项目"、"联系我"链接

---

### Requirement: 平滑滚动到对应 Section

点击导航链接后页面平滑滚动到目标 Section。

- 点击"首页"滚动到 `#home`
- 点击"项目"滚动到 `#projects`
- 点击"联系我"滚动到 `#contact`
- 滚动行为使用 `smooth`

#### Scenario: 点击导航链接

- **GIVEN** 导航栏已加载
- **WHEN** 用户点击"项目"链接
- **THEN** 页面平滑滚动到 `#projects` 区域

#### Scenario: 目标 Section 不存在

- **GIVEN** 页面中不存在 `#contact` 元素
- **WHEN** 用户点击"联系我"链接
- **THEN** 不发生滚动，不抛出异常，页面保持当前状态

---

### Requirement: 背景模糊效果

导航栏具有毛玻璃（Glassmorphism）视觉效果。

- 背景使用半透明颜色
- 应用 `backdrop-filter: blur()` 实现背景模糊
- 模糊效果在亮/暗模式下均生效

#### Scenario: 导航栏背景模糊生效

- **GIVEN** 导航栏已加载
- **WHEN** 用户滚动页面，内容在导航栏下方经过
- **THEN** 导航栏背景呈现毛玻璃模糊效果
- **AND** 导航栏文字内容清晰可读

#### Scenario: 浏览器不支持 backdrop-filter

- **GIVEN** 用户使用不支持 `backdrop-filter` 的浏览器
- **WHEN** 页面加载
- **THEN** 导航栏显示为纯半透明背景
- **AND** 文字内容不受影响

---

### Requirement: 亮/暗模式适配

导航栏的颜色在亮/暗模式下自适应。

- 亮色模式使用浅色半透明背景
- 暗色模式使用深色半透明背景
- 导航栏文字色在主题切换时同步变化

#### Scenario: 主题切换影响导航栏

- **GIVEN** 导航栏当前为亮色模式
- **WHEN** 用户切换到暗黑模式
- **THEN** 导航栏背景和文字颜色切换为暗黑模式配色

#### Scenario: 初始主题匹配

- **GIVEN** 用户系统设置为暗黑模式
- **WHEN** 页面加载
- **THEN** 导航栏直接使用暗黑模式配色，无闪烁
