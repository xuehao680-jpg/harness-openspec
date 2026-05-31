## MODIFIED Requirements

### Requirement: CTA 按钮跳转到项目区域

Hero 区域内包含一个 CTA 按钮，点击后页面平滑滚动到项目展示区。

- 按钮文字可配置
- 点击后定位到 `#projects` 元素（项目展示区）
- 滚动行为使用 `smooth`

#### Scenario: 点击 CTA 按钮

- **GIVEN** 用户停留在 Hero Section
- **WHEN** 用户点击 CTA 按钮
- **THEN** 页面平滑滚动到项目展示区（`#projects`）
