## MODIFIED Requirements

### Requirement: 导航栏内容布局

导航栏左侧显示站点名称，右侧显示导航链接。

- 站点名称与 Hero 中的姓名一致
- 导航链接包含：首页、关于、项目、联系我
- 使用 Flexbox 左右布局

#### Scenario: 正常显示导航栏内容

- **GIVEN** 导航栏已加载
- **WHEN** 用户查看页面顶部
- **THEN** 左侧显示站点名称
- **AND** 右侧依次显示"首页"、"关于"、"项目"、"联系我"链接

---

### Requirement: 平滑滚动到对应 Section

点击导航链接后页面平滑滚动到目标 Section。

- 点击"首页"滚动到 `#home`
- 点击"关于"滚动到 `#about`
- 点击"项目"滚动到 `#projects`
- 点击"联系我"滚动到 `#contact`
- 滚动行为使用 `smooth`

#### Scenario: 点击导航链接

- **GIVEN** 导航栏已加载
- **WHEN** 用户点击"关于"链接
- **THEN** 页面平滑滚动到 `#about` 区域
