## ADDED Requirements

### Requirement: Hero 区域全屏展示

Hero Section 在视口中占满全屏高度，内容在水平和垂直方向居中。

- 高度使用 `100dvh`，降级使用 `100vh`
- 内容在水平和垂直方向均居中
- Hero 区域的层级：底层为 CSS 渐变背景，中层为 Canvas 粒子层，上层为文字内容

#### Scenario: 在标准视口下显示全屏 Hero

- **GIVEN** 用户访问网站首页
- **WHEN** 页面加载完成
- **THEN** Hero Section 的高度等于视口高度
- **AND** 内容在水平和垂直方向居中

#### Scenario: 在 iOS Safari 下显示全屏 Hero

- **GIVEN** 用户在 iOS Safari 浏览器中访问网站
- **WHEN** 页面加载完成
- **THEN** Hero Section 不被地址栏和底部工具栏遮挡
- **AND** 高度解析为 `100dvh`

---

### Requirement: 个人身份信息展示

Hero 区域内展示个人身份信息，包含三项内容：姓名、职业/头衔、一句话介绍。

- 姓名使用大字号标题
- 职业/头衔使用中等字号
- 一句话介绍使用较小字号，支持换行

#### Scenario: 正常显示三项身份信息

- **GIVEN** Hero Section 已加载
- **WHEN** 用户查看 Hero 区域
- **THEN** 姓名、职业/头衔、一句话介绍按顺序从上到下显示

#### Scenario: 一句话介绍内容超长

- **GIVEN** 一句话介绍文本长度超过一行
- **WHEN** 在移动端视口下渲染
- **THEN** 文本自动换行，不溢出容器

---

### Requirement: CTA 按钮跳转到项目区域

Hero 区域内包含一个 CTA 按钮，点击后页面平滑滚动到项目区域。

- 按钮文字可配置
- 点击后定位到 `#projects` 元素
- 滚动行为使用 `smooth`

#### Scenario: 点击 CTA 按钮

- **GIVEN** 用户停留在 Hero Section
- **WHEN** 用户点击 CTA 按钮
- **THEN** 页面平滑滚动到项目区域（`#projects`）

#### Scenario: 项目区域尚不存在

- **GIVEN** 页面中不存在 `#projects` 元素
- **WHEN** 用户点击 CTA 按钮
- **THEN** 不发生滚动，不抛出异常，页面保持当前状态

---

### Requirement: 科技感粒子渐变背景

Hero 背景由两层组成：底层为 CSS 渐变色，上层为 Canvas 绘制的静态粒子图案。

- 渐变色在 CSS 中定义，支持亮/暗两套色值
- Canvas 粒子缓慢漂移运动（0.1~0.4 px/frame），营造科技感动态效果
- Canvas 覆盖整个 Hero 区域
- Canvas 粒子不遮挡文字内容的可读性
- 粒子位置在窗口 resize 后重新计算绘制

#### Scenario: 正常渲染粒子背景

- **GIVEN** Hero Section 已加载
- **WHEN** 页面渲染完成
- **THEN** 背景显示 CSS 渐变色
- **AND** 渐变色上方叠加有 Canvas 粒子图案
- **AND** 文字内容清晰可见，不被粒子遮挡

#### Scenario: 浏览器不支持 Canvas

- **GIVEN** 用户使用的浏览器不支持 Canvas（极罕见情况）
- **WHEN** 页面加载
- **THEN** 页面退化显示为纯 CSS 渐变背景
- **AND** 文字内容不受影响

#### Scenario: 窗口尺寸变化

- **GIVEN** Hero Section 已渲染粒子背景
- **WHEN** 用户调整浏览器窗口大小
- **THEN** Canvas 粒子按新尺寸重新绘制
- **AND** 重新绘制在 resize 结束后 200ms 内完成

#### Scenario: 用户开启减少动效

- **GIVEN** 用户在系统设置中开启了"减少动效"（prefers-reduced-motion: reduce）
- **WHEN** 页面加载
- **THEN** 粒子保持静态，不产生漂移运动

#### Scenario: 标签页切换

- **GIVEN** Hero Section 粒子正在动画中
- **WHEN** 用户切换到其他标签页
- **THEN** 粒子动画暂停，不消耗 CPU
- **AND** 用户切回标签页时动画恢复

---

### Requirement: 明亮/暗黑模式切换

Hero Section 自动响应系统主题偏好，并支持手动切换。

- 默认跟随系统主题（`prefers-color-scheme`）
- CSS 渐变背景在亮/暗模式下使用不同的色值
- Canvas 粒子颜色在亮/暗模式下使用不同的色值
- 切换主题时 Canvas 重新绘制以匹配新配色

#### Scenario: 跟随系统主题

- **GIVEN** 用户系统设置为暗黑模式
- **WHEN** 页面加载
- **THEN** Hero 背景使用暗黑模式配色方案
- **AND** 文字颜色自动调整为浅色

#### Scenario: 手动切换主题

- **GIVEN** Hero Section 当前显示为亮色模式
- **WHEN** 用户通过切换按钮切换到暗黑模式
- **THEN** Hero 背景切换为暗黑模式配色
- **AND** Canvas 粒子以新颜色重新绘制
- **AND** 切换后主题偏好持久化，刷新页面后保持

#### Scenario: 主题切换时的 Canvas 闪烁

- **GIVEN** Hero Section 使用暗黑模式
- **WHEN** 用户切换为亮色模式
- **THEN** CSS 渐变和粒子颜色同步变化
- **AND** 不会出现粒子颜色与渐变不匹配的闪烁瞬间
