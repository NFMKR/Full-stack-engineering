**「页面风格指南 设计系统文档」**
- 提示词：帮我基于这个风格设计一个 XXX 页面
--- 

- 目录:
* 概述
* 色彩系统（Brand / Semantic / Neutral）
* 字体排版系统
* 圆角规范
* 阴影系统
* 组件外观规范（按钮、卡片、输入框、表格等）
* 间距系统（Spacing Scale）
* 图标规范
* 动画系统
* 响应式规范
* 交互状态（Hover/Active/Disabled）
* 布局规则

---

# 📘 Web 产品 设计系统（Design System）

---

# 1. 品牌设计基础（Brand Foundation）

- 概述：本产品是一款面向 [目标用户类型，例如：中小企业、工业企业、SaaS平台用户] 的 Web 端业务系统。
主要目标是提供 高效、可视化、易操作 的界面体验，主要有这些模块：xxx,yyyy,zzzz。
---

## 1.1 品牌主色（Brand Colors）

### ========= PRIMARY =========

| 名称            | 代码        | 用途             |
| ------------- | --------- | -------------- |
| Primary       | `#165DFF` | 按钮、链接、主视觉、品牌标识 |
| Primary Hover | `#3C7DFF` | 鼠标悬停           |
| Primary Light | `#E8F0FF` | 浅背景、弱分割线       |
| Primary Dark  | `#0A3ABF` | 激活状态、深背景       |

---

### ========= SECONDARY =========

| 名称        | 代码        | 说明      |
| --------- | --------- | ------- |
| Secondary | `#36CFC9` | 次要亮色点缀  |
| Accent    | `#FF9F43` | 轻量提示、装饰 |

---

## 1.2 中性色（Neutral Colors）

| 名称          | 代码        | 用途      |
| ----------- | --------- | ------- |
| Text Dark   | `#1E293B` | 标题文字    |
| Text Normal | `#334155` | 正文      |
| Text Light  | `#64748B` | 辅助文字    |
| Border      | `#E2E8F0` | 边框、分割线  |
| Bg Light    | `#F8FAFC` | 浅背景区块   |
| White       | `#FFFFFF` | 卡片/内容白底 |

---

## 1.3 语义色（Semantic Colors）

| 类型      | Normal    | Hover     | Background |
| ------- | --------- | --------- | ---------- |
| Success | `#16A34A` | `#22C55E` | `#E8F8EF`  |
| Warning | `#F59E0B` | `#FBBF24` | `#FFF7E6`  |
| Error   | `#DC2626` | `#EF4444` | `#FDEDED`  |
| Info    | `#165DFF` | `#3C7DFF` | `#E8F0FF`  |

---

# 2. 字体排版系统（Typography System）

---

## 2.1 字体（Font Family）

```
"Inter", "PingFang SC", "Microsoft YaHei", "Helvetica Neue", Arial, sans-serif
```

---

## 2.2 字号与层级（Font Scale）

| 层级      | 类名（Tailwind）                                     | 用途        |
| ------- | ------------------------------------------------ | --------- |
| Display | `text-[clamp(2.5rem,6vw,4rem)] font-bold`        | 大屏 Banner |
| H1      | `text-[clamp(2rem,5vw,3.5rem)] font-bold`        | 大标题、Hero  |
| H2      | `text-[clamp(1.75rem,4vw,2.5rem)] font-semibold` | 区域标题      |
| H3      | `text-xl md:text-2xl font-semibold`              | 小标题       |
| Body    | `text-base text-gray-700`                        | 正文        |
| Small   | `text-sm text-gray-500`                          | 说明文字      |

---

## 2.3 行高（Line Height）

* 标题：`leading-tight`
* 正文：`leading-relaxed`
* 多段落：`leading-loose`

---

# 3. 间距系统（Spacing System）

采用 4px 基础设计单位。

| 间距名称 | tailwind 类    | px   |
| ---- | ------------- | ---- |
| xs   | `p-1` / `m-1` | 4px  |
| sm   | `p-2`         | 8px  |
| md   | `p-4`         | 16px |
| lg   | `p-6`         | 24px |
| xl   | `p-8`         | 32px |
| 2xl  | `p-10`        | 40px |
| 3xl  | `p-12`        | 48px |

---

## 3.1 Section 区块标准

用于页面拆分区：

```
padding-top: 80px (md 120px)
padding-bottom: 80px (md 120px)
```

Tailwind：

```
pt-20 md:pt-32 pb-20 md:pb-32
```

---

# 4. 圆角系统（Border Radius System）

| 名称   | 类名             | 数值     |
| ---- | -------------- | ------ |
| 小圆角  | `rounded-md`   | 6px    |
| 默认   | `rounded-lg`   | 12px   |
| 大圆角  | `rounded-xl`   | 16px   |
| 特大圆角 | `rounded-2xl`  | 24px   |
| 完全圆形 | `rounded-full` | 9999px |

全局默认使用 **rounded-lg**。

---

# 5. 阴影系统（Shadow System）

| 类名        | 效果          |
| --------- | ----------- |
| shadow-sm | 轻微，按钮 hover |
| shadow-md | 卡片默认        |
| shadow-lg | 卡片 hover    |
| shadow-xl | Hero 大卡片使用  |

卡片必须使用：

```
rounded-2xl shadow-md hover:shadow-lg transition-all
```

---

# 6. 交互规范（Interaction）

---

## 6.1 Hover / Active / Disabled

### 按钮（Primary）

| 状态       | 样式                                           |
| -------- | -------------------------------------------- |
| Normal   | bg-primary text-white                        |
| Hover    | bg-primary-hover                             |
| Active   | scale-[0.98]                                 |
| Disabled | bg-gray-300 text-gray-500 cursor-not-allowed |

---

## 6.2 输入框（Input）

```html
border border-gray-300 rounded-lg px-4 py-2
focus:border-primary focus:ring-primary
```

---

## 6.3 卡片 Hover

```
hover:shadow-lg hover:-translate-y-1
transition-all
```

---

## 6.4 可点击元素

必须包含：`cursor-pointer`
并提供：

* hover color
* hover opacity
* hover underline (对于链接)

---

# 7. 图标系统（Iconography）

---

## 7.1 图标来源

统一使用：

```
Iconify (官方 Vue 组件)
```

尺寸规范：

* 默认：`24px`
* 小：`20px`
* 大：`32px`

颜色规范：

* 默认：`currentColor`
* 不允许硬编码十六进制

---

# 8. 组件设计规范（最关键部分）

以下是整个产品 UI 组件的统一标准。

---

## 8.1 按钮（Button）

### 视觉规范

* 圆角：`rounded-lg`
* 文字：`font-medium`
* 高度：`h-12`
* 内间距：`px-6`

### 主按钮（Primary）

```html
bg-primary text-white hover:bg-primary-hover shadow-sm
```

### 次按钮（Secondary）

```html
bg-white text-primary border border-primary hover:bg-primary/5
```

### 禁用按钮

```html
bg-gray-200 text-gray-500 cursor-not-allowed
```

---

## 8.2 输入框（Input）

```html
w-full border border-gray-300 rounded-lg px-4 py-3
focus:ring-2 focus:ring-primary focus:border-primary
```

---

## 8.3 卡片（Card）

```html
bg-white rounded-2xl shadow-md p-6
hover:shadow-lg hover:-translate-y-1 transition-all
```

---

## 8.4 表格（Table）

* 标题行背景：`bg-gray-50`
* 行 hover：`hover:bg-gray-50`
* 单元格间距：`px-4 py-3`
* 边框：`border-b border-gray-200`

---

## 8.5 标签（Tag）

```
inline-flex px-3 py-1 rounded-full text-sm
bg-primary-light text-primary
```

---

## 8.6 Modal 弹窗

背景遮罩：

```
bg-black/50 fixed inset-0 flex items-center justify-center
```

弹窗主体：

```
bg-white rounded-2xl shadow-xl p-6 w-[90%] max-w-lg
```

---

# 9. 动画系统（Motion）

默认动画：

```
transition-all duration-300 ease-in-out
```

进入动画（如卡片 / modal）：

```
animate-fadeIn
animate-slideUp
```

AI 生成时必须添加合理的动画修饰。

---

# 10. 布局系统（Layout）

---

## 10.1 Container 宽度

```
max-width: 1200px
margin: 0 auto
padding-left/right: 16px → 24px → 32px
```

Tailwind：

```
px-4 sm:px-6 lg:px-8
```

---

## 10.2 栅格系统

```html
grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 gap-6
```

---

## 10.3 Flex 规范

```
flex flex-col lg:flex-row items-center gap-10
```

---

# 11. 响应式规则（Responsive）

---

### 移动端优先

* 一切从手机 UI 起步（Mobile First）
* Desktop 才做横向布局

### 大断点逻辑

| 尺寸   | 行为        |
| ---- | --------- |
| sm < | 列布局       |
| md < | 卡片两列      |
| lg < | Hero 左右布局 |

---

# 12. Hero Banner 规范（非常重要）

**AI 必须严格遵守：**

* 左：标题 + 文案 + 按钮
* 右：插图
* 移动端：插图隐藏，背景图改用 background-image 填充
* 背景图必须使用：

```
bg-cover bg-center bg-no-repeat
```

---

# 13. 插图（Illustration）规范

* 风格统一（线性/渐变/3D 统一一种）
* 图像必须保持左右占满，不允许出现“白边”
* 使用矢量或高分辨率 PNG
* 不允许拉伸变形

---

# 14. 可访问性（A11y）

* 图片必须写 `alt`
* 颜色对比必须符合 WCAG AA
* 表单必须有 label
* 键盘可操作性（tab 顺序）

---

# 15. 文案风格（Content Style）

* 专业、直接、有逻辑
* 避免口语
* 避免长句
* 多用动词导向：

  * 分析、诊断、生成、优化
* 多用价值导向句：

  * 提升、降低、减少、提高效率

---