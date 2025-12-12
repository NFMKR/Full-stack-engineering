**面向移动端 App 的产品/设计通用指南规范**，专为在使用 AI 生成代码或协作开发时提高产出质量而设计。内容覆盖视觉、交互、可访问性、前端实现约定、资源规范、测试与验收、以及给 AI 的 Prompt 范本，便于你把规范直接喂给 AI 或用于团队交付。

> 目标：
>
> * 让设计到代码（尤其是 AI 生成代码）可复现、可校验、可维护。
> * 降低视觉/交互偏差，提高交付一致性。
> * 提升开发效率并保障产品可用性与易用性。

---

# 移动端 App 设计通用指南（实用版）

## 目录（快速导航）

1. 总体原则
2. 视觉系统（色彩、排版、图标、间距、圆角、阴影）
3. 布局与栅格（移动优先）
4. 组件规范（按钮、表单、列表、卡片、导航）
5. 交互与动效（Motion）
6. 可访问性（A11y）与国际化（i18n）
7. 资源与图像规范（切图、分辨率、命名）
8. 设计到代码交付（token、tailwind/vars、组件目录）
9. AI 生成与校验工作流（Prompt 模板 + 校验清单）
10. 测试、验收与上线前检查清单
11. 附录：常用尺寸/间距/颜色 token 列表

---

## 1. 总体设计原则（必须牢记）

* **移动优先（Mobile First）**：从 360–414px 宽度开始设计与验证。
* **简洁可控**：尽量减少布局分支与复杂样式，便于 AI 重复生成相同结果。
* **视觉一致性**：颜色、间距、圆角、阴影应由 Token 控制，所有组件引用 token。
* **易用性优先**：交互明确、反馈及时、可触达元素目标区域需≥44×44dp。
* **可校验性**：设计交付必须包含 token、组件变体、交互说明与验收准则，便于自动化校验/AI 校审。

---

## 2. 视觉系统

### 2.1 颜色（建议以 token 管理）

* 主色 Primary：`--color-primary: #165DFF`
* 主色 Hover/Active：`--color-primary-600: #0A3ABF`
* 中性：`--color-900: #111827`、`--color-700: #374151`、`--color-500: #6B7280`、`--color-200: #E5E7EB`
* 背景：`--color-bg: #FFFFFF` 或深色主题对应 token
* 成功/警告/错误：`--color-success: #16A34A`、`--color-warning: #F59E0B`、`--color-error: #EF4444`

> **要求**：所有颜色在设计稿与代码里都使用 token 命名，不允许硬编码十六进制。

### 2.2 字体与排版

* 主字体（中文）：`PingFang SC / 思源黑体`；英文字体：`Inter / Roboto`
* 字级建议（移动端）：

  * Title / Display：20–28sp（H1）
  * Section Title：16–20sp（H2）
  * Body：14–16sp（正文）
  * Caption：12sp（注释）
* 行高建议：正文 1.4–1.6；标题 1.1–1.3
* 文本层级应使用 typographic token：`--font-size-xxl`、`--font-size-xl`、`--font-size-md`...

### 2.3 圆角、阴影、边框

* 圆角：基础 `8px`，小控件 `6px`，卡片 `12–16px`，浮层 `16–24px`。
* 阴影：尽量简约，生产环境用 1–2 个阴影层级（light/medium）。
* 边框：默认 1px（`--border-color` 使用中性 token）。

### 2.4 图标

* 使用矢量图标（SVG）并生成多分辨率导出（24/32/40）。
* 命名规范：`ic_<category>_<name>_24.svg`（如 `ic_action_search_24.svg`）。

---

## 3. 布局与栅格（Mobile First）

* 布局基线宽度：`360`、`375`、`414` 三个常见机型都应测试。
* 水平间距基准（Spacing Scale，基于 4px）：`4,8,12,16,20,24,32,40`。
* Container 横向 padding：通常 `16px`（`px-4`），大屏可到 `24px`。
* 列与网格：移动端使用单列或 2 列卡片布局（宽度自适应），避免在小屏出现 3 列。

---

## 4. 组件规范（每个组件都要包含：用法、props、variant、state、交互、可访问性）

### 4.1 Button（按钮）

* 尺寸：大 `44–48px`（主操作），中 `36–40px`（次要）。
* 触控目标：≥44×44dp。
* 状态：Default / Hover / Pressed / Disabled / Loading。
* Variant：Primary / Secondary / Ghost / Link。
* Icon 按钮：图标 + label 或仅图标，图标 padding 对称。
* 样式示例（token）：

  * `btn-primary-bg: var(--color-primary)`
  * `btn-primary-color: #fff`
  * `btn-radius: 8px`

### 4.2 Input / Form

* Label 在上方（mobile 优先），必要时使用 floating label。
* 校验提示：错误用 `--color-error`，帮助文本使用 `--color-500`。
* 输入框高度：40–48px，左右内边距 `12–16px`。
* 文件上传、选择器需支持可键盘/可触控交互。

### 4.3 List / Item / Card

* 列表间距 8–12px，项目高度 56–80px（根据所含信息）。
* 列表项应支持 swipe（删除/更多）交互，提供明确的撤销策略。
* 卡片：margin/padding 使用 token，背景及阴影使用 token。

### 4.4 Navigation（导航）

* 顶部导航（Top Bar）：高度 56–64px；常驻顶部或滚动隐藏。
* 底部导航（Tab Bar）：高度 56px，图标+label，tap target ≥44px。
* Drawer：从左/右侧滑出覆盖层，最大宽度 320–360px（手机）。

### 4.5 Modal / Sheet（弹层）

* Modal 覆盖必须包含遮罩（opacity 0.5），ESC 或点击遮罩关闭（可选）。
* 底部弹出 Sheet：常用于操作、选择，height ≤ 80% 屏幕，顶部留 16px radius。

---

## 5. 交互与动效（Motion）

* 动效原则：快速（<=200ms）→自然 → 可中断。
* 常用动效：

  * 按钮按下：scale 0.98，duration 120ms
  * 弹出：opacity 0 → 1 + translateY 8px → 0, duration 200–260ms
  * 列表项滑出：translateX，伴随 opacity 变化
* 使用硬件加速的属性（transform、opacity），避免 expensive 属性（width/height/left/top）导致卡顿。
* 为重要交互提供“取消”或“撤销”机制（尤其是 destructive 操作）。

---

## 6. 可访问性（A11y）与国际化（i18n）

* 所有交互元素必须可被屏幕阅读器识别（button、input 等需正确 ARIA 标签）。
* 字体大小应支持系统字体缩放（避免 fixed px 仅使用 rem/sp/em）。
* 颜色对比度符合 WCAG AA（文本对比至少 4.5:1），重要按钮和正文尤其要注意。
* 支持 RTL（从右到左语言）和多语言替换（文案以键值形式管理）。
* 文本长度预留：UI 需防止因多语言导致布局溢出（eg. 德语/俄语通常更长）。

---

## 7. 资源与图像规范

* 图像：优先 SVG（图标/矢量）；位图使用 WebP（支持）或 2x PNG。
* 移动端图像切图：针对 1x/2x/3x（密度）导出。
* 命名规范（统一且可读）：`/assets/images/home_banner@2x.webp`、`/assets/icons/ic_search_24.svg`。
* 文件大小控制：单张图片尽量 <200KB（首屏更小）。
* 插图/人物照遵守公司合规（肖像权、版权）。

---

## 8. 设计到代码交付（对 AI 与前端工程化的具体指导）

* **Token 管理**：所有颜色、字号、间距、radius、shadow 等以 token 表形式维护（JSON/YAML）。示例：

```json
{
  "color": { "primary": "#165DFF", "bg": "#FFFFFF" },
  "spacing": { "sm": 8, "md": 16, "lg": 24 },
  "radius": { "base": 8, "card": 12 }
}
```

* **组件目录建议**（Vue3 项目）：

```
/src/components/
  /ui/    (Button/Input/Modal)
  /layout/ (Header/Footer/TabBar)
  /blocks/ (Hero/Feature/Carousel)
```

* **命名约定**：组件 PascalCase（`AppButton.vue`），CSS class 使用 BEM 或 Tailwind utilities。
* **样式策略**：优先使用 utility-first（Tailwind）或 CSS variables + design tokens，避免孤立 style。
* **Storybook / Component Library**：每个组件必须有 story（含 states/variants），便于 AI 校验与自动化测试。

---

## 9. AI 生成与校验工作流（实操）

### 9.1 AI 生成原则（Prompt 结构）

* **上下文**（project tokens + component variants）
* **目标**（期望输出：Vue3 `<script setup>` + TS + tailwind class）
* **约束**（不要使用外部库、禁止硬编码颜色、必须使用 tokens、文件命名）
* **输出格式**（文件名/代码块/测试用例/Storybook）
* **示例 Prompt**：

```
请基于以下 token: {"color.primary":"#165DFF", ...} 生成一个 Vue3 Button 组件：
- 使用 <script setup lang="ts">，Props: {type: 'primary'|'secondary', size: 'lg'|'md'}。
- 必须用 tailwind utility 或 CSS var，不允许十六进制直接写在组件。
- 返回：Button.vue, Button.stories.ts, Button.test.ts (vitest)
```

### 9.2 AI 生成输出必须附带的清单（交付物）

* 组件代码（带 types）
* CSS token 引用（或 tailwind class）
* Storybook story（包含主要状态）
* 单元测试（覆盖主要行为）
* 简短使用文档（README snippet）

### 9.3 自动化校验清单（AI 输出后自动或人工复核）

* 颜色/间距是否使用 token？（自动脚本检测）
* 是否符合触控面积 ≥44×44？（静态检查）
* 是否包含 aria 属性与可访问性？（lint）
* 是否包含 Story 和基本测试？（CI 检查）
* CI 运行：lint+typecheck+test 必过。

---

## 10. 测试、验收与上线前检查清单（Release Checklist）

* [ ] UI 与设计稿像素级对齐（关键页面）
* [ ] Storybook 覆盖所有组件状态
* [ ] 单元测试覆盖关键逻辑（≥70%）
* [ ] e2e (Playwright) 覆盖主流程（登录、提交、导航）
* [ ] 性能检查（首次可交互 ≤ 2s，资源大小控制）
* [ ] 可访问性扫描（axe-core）通过基本规则
* [ ] 多语言、RTL 测试完毕
* [ ] 断网/弱网场景测试（接口超时处理/离线体验）
* [ ] 上线监控 hook（Sentry / RUM）已集成

---

## 11. 附录：常用 Token（示例）

```json
{
  "color": {
    "primary": "#165DFF",
    "primary-600": "#0A3ABF",
    "bg": "#FFFFFF",
    "text": "#111827",
    "muted": "#6B7280",
    "danger": "#EF4444",
    "success": "#16A34A"
  },
  "spacing": { "xs": 4, "sm": 8, "md": 16, "lg": 24, "xl": 32 },
  "radius": { "sm": 6, "base": 8, "lg": 12, "xl": 16 },
  "fontSize": { "xl": 20, "lg": 16, "md": 14, "sm": 12 }
}
```

---

# 附：常用 AI Prompt 模板（可直接复制）

### 生成组件（Button）Prompt

```
你是前端开发助手。基于以下 design tokens:
{ "color.primary":"#165DFF", "radius.base":"8px", "spacing.md":16 }
请生成一个 Vue3 组件 `AppButton.vue`（<script setup lang="ts">）：
- Props: { type?: 'primary'|'secondary', size?: 'lg'|'md', disabled?: boolean }
- 必须使用 tailwind utility 或 css var（不能使用硬编码色值）。
- 输出文件：组件代码 + 对应 Storybook story + vitest 单元测试（覆盖点击与 disabled）。
- 代码风格：TS 严格模式，函数与变量命名驼峰。
```

### 生成页面（Hero）Prompt

```
使用 tokens: { ... }，请生成一个移动端 Hero 区块：
- 图片为 assets/mobile/banner_mobile@2x.webp（已存在）
- 文本放在左半屏宽（w-1/2），不换行（whitespace-nowrap），字体使用 token fontSize.xl
- CTA 两个按钮竖排：primary（主色）与 secondary（白底边框）
- 返回 Vue3 页面组件、样式引用、以及用于 Storybook 的 mock data
```

---

# 结语（如何开始落地）

1. 把此规范以 `design-tokens.json` 与 `style-guideline.md` 的形式加入项目仓库。
2. 在 CI 中增加 token 检查脚本与 Storybook 校验，保障 AI 生成代码合规。
3. 从小组件开始（Button/Input/Modal）用 AI 生成并在 Storybook 中复核，逐步扩展组件库。
4. 建立每次 AI 生成后的“自动化校验+人工验收”流程，形成持续迭代的闭环。

---