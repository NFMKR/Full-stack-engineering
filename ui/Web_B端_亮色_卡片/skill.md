# 项目主题与样式使用指引

## 项目主题风格

本项目为 B 端 Web 系统，整体风格定位：
现代简约、干净舒适、专业克制、高可读性
视觉基调：纯白背景 + 白色柔和卡片 + 细浅边线 + 品牌红点缀
整体视觉轻盈、透气、不拥挤、不刺眼。

## 统一样式标准（必须严格遵守）

所有页面、组件、布局、文字、颜色必须使用 style_global.css 内定义的变量，禁止直接写死色值、尺寸、间距。

## 样式文件使用规则

1. 页面背景统一使用 --bg-page
2. 卡片、面板、弹窗背景统一使用 --bg-card
3. 所有边框、分割线统一使用 --border-1 或 --border-card
4. 圆角统一使用：
   小元素（按钮/输入框）：--radius-sm (10px)
   卡片/面板：--radius-md (12px)
   大面板/弹窗：--radius-lg (16px)
5. 文字颜色层级：
   主要标题：--text-primary
   次要文字：--text-secondary
   辅助文字：--text-muted
   强调文字：--text-black-emphasis
6. 品牌色系（红色）仅用于强调、选中状态、主按钮，禁止大面积使用：
   主色：--accent-primary
   深色：--accent-strong
   浅色：--accent-soft
   背景色：--accent-bg
   边框色：--accent-border
7. 阴影层级：
   普通卡片：--shadow-card
   紧凑卡片：--shadow-card-tight
   悬停效果：--shadow-card-hover
   弹窗阴影：--shadow-modal

## AI 生成代码要求

1. 所有样式必须引用 CSS 变量，不允许写死数值
2. 保持风格统一、干净、简约、舒适
3. 禁止使用花哨效果、厚重阴影、强对比色
4. 保持页面层级清晰、交互克制
5. 优先使用卡片式布局，适当留白
