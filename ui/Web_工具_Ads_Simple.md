 -----
# [工具类 Web + Ads] 设计与开发规范指南 (`DESIGN_SYSTEM_TOOLING.md`)

**[指令]**：你是本项目 word在线转化pdf文档（工具类网站）的前端架构师。在开发时，必须严格遵循以下视觉规范、布局逻辑和广告位处理策略。

## 1\. 核心定调 (The Vibe)

  * **关键词**：[功能至上、视觉降噪、高明度、极速响应]
  * **视觉隐喻**：[瑞士军刀般的精密与整洁]
  * **核心体验**：
      * **输入前**：清晰的引导与留白。
      * **处理中**：明确的加载反馈（骨架屏）。
      * **输出后**：高对比度结果展示，提供“一键复制”等快捷操作。
  * **适配策略**：以 **1440×900** (桌面标准) 为设计基准，向下兼容平板与手机，确保手机端也功能与广告等适配正常，向上适配大屏。

## 2\. 视觉规范 (Visual Specs)

### A. 色彩体系 (CSS Variables)

*增加了功能状态色（成功/失败）和广告占位色。*

```css
:root {
    /* --- 背景体系 --- */
    --bg-core:    #FFFFFF; /* 核心背景 */
    --bg-sub:     #F9FAFB; /* 次级背景 (侧边栏/底色) */
    --bg-input:   #FFFFFF; /* 输入框背景 */
    --bg-ad:      #F3F4F6; /* 广告位占位背景 (灰色斜纹) */

    /* --- 强调色 (工具类需克制) --- */
    --accent-primary: #2563EB; /* 核心操作 (如: 生成、转换) */
    --accent-hover:   #1D4ED8;
    
    /* --- 状态色 (工具反馈必备) --- */
    --state-success:  #10B981; /* 成功/结果 */
    --state-error:    #EF4444; /* 错误/警告 */
    --state-warn:     #F59E0B; /* 提示 */

    /* --- 文字体系 --- */
    --text-main:  #111827; /* 标题/输入内容 */
    --text-body:  #4B5563; /* 说明文案 */
    --text-dim:   #9CA3AF; /* Placeholder/辅助 */
    --text-link:  #2563EB; /* 链接 */

    /* --- 边框 --- */
    --border-line:   #E5E7EB;
    --border-focus:  rgba(37, 99, 235, 0.4); /* 输入框聚焦光环 */
}
```

### B. 排版与字体 (Typography)

*工具类必须引入等宽字体用于显示代码、ID 或数据。*

  * **字体家族**：
      * UI: `Inter`, `思源黑体`, sans-serif
      * **Code/Data**: `'JetBrains Mono'`, `'Fira Code'`, monospace (**新增**)
  * **字号策略**：
      * 输入框文字：`1rem` (16px) - *防止 iOS 缩放*
      * 工具结果：`1.125rem` (18px) - *突出显示*
      * 标签/辅助：`0.875rem` (14px)

### C. 材质与组件质感

  * **卡片/容器**：
      * `background: #FFFFFF; border: 1px solid var(--border-line); border-radius: 8px;`
      * *去除了磨砂玻璃，工具类追求实色背景以提高文字可读性。*
  * **输入框 (Input/Textarea)**：
      * 常态：`border: 1px solid #D1D5DB; bg: #FFF;`
      * Focus：`border-color: var(--accent-primary); box-shadow: 0 0 0 3px var(--border-focus);` (强调聚焦)
  * **投影**：仅用于悬浮层 (Dropdown/Modal)，主界面尽量扁平化以减少渲染负担。

### D. 图标样式（Icon）

  * **风格**：线性图标（stroke-width: 2），简洁统一，无多余装饰
  * **尺寸**：导航图标：20×20px  按钮图标：18×18px  表单 / 状态图标：16×16px  数据指标图标：24×24px
  * **颜色**：默认与当前文本颜色一致，强调图标使用 --brand-accent 或对应状态色

## 3\. 布局与响应式策略 (Layout & Responsive)

### A. 断点系统 (Breakpoints)

*基于用户指定的设备尺寸定义 CSS Media Queries。*

  * **Desktop L**: `≥ 1920px` (增加两侧留白)
  * **Desktop S (基准)**: `≥ 1440px` (完美布局)
  * **Laptop/Tablet L**: `1024px - 1439px` (侧边栏可能收起)
  * **Tablet Portrait**: `768px - 1023px` (广告位转为底部/顶部)
  * **Mobile**: `< 768px` (单栏布局，隐藏非核心修饰)

### B. 核心布局结构 (Holy Grail Layout)

工具页采用 **"T型"** 或 **"三栏"** 结构：

1.  **Header (56px-64px)**: Logo + 导航 + 搜索。
2.  **Container (Max-width: 1440px)**:
      * **Left (工具区, flex: 1)**: 核心操作区域。
      * **Right (广告/推荐区, width: 320px)**: *Desktop 可见，Tablet/Mobile 隐藏或移至底部。*

### C. 广告位预留规范 (Ads Specs)

*严格遵循 IAB 标准尺寸，避免布局抖动 (CLS)。*

  * **Top Banner (顶部通栏)**:
      * Desktop: `728x90`
      * Mobile: `320x50` (Sticky 底部或顶部)
  * **Sidebar Box (侧边栏矩形)**:
      * Desktop: `300x250` 或 `300x600`
      * Tablet/Mobile: 隐藏侧边栏广告，转为内容流间广告 (In-feed)。
  * **占位处理**:
      * 开发阶段必须渲染一个 `div`，背景色为 `var(--bg-ad)`，并标明 "Ad Space"。
      * CSS: `min-height: [对应高度];` *防止广告加载时页面跳动。*

## 4\. 工具类 UI 细节指南 (Tool UI Details)

### A. 输入区 (Input Area)

  * **布局**: 标签 (Label) 在上方，输入框在下方。
  * **清空按钮**: 输入框右上角必须预留 "Clear" 或 "Reset" 按钮。
  * **操作栏**: “生成/转换”按钮应为全宽 (Mobile) 或 右侧固定 (Desktop)，突出显示。

### B. 结果区 (Result Area)

  * **只读属性**: 结果框必须是 `readonly` 或 `<pre><code>` 标签。
  * **快捷操作**: 必须配备 **"Copy" (复制)** 按钮，点击后给予 `Tooltip` 反馈 ("Copied\!")。
  * **空状态**: 当未输入时，结果区显示引导插画或灰色占位符，不可留白。

### C. 加载状态 (Loading)

  * **骨架屏 (Skeleton)**: 禁止使用全屏 Loading 转圈。应在结果区域显示波动的灰色色块，暗示“正在计算”。

### D. 订阅/定价页规范（Pricing & Subscription Module）

**[目标]**：订阅页面，不要出现布局重叠与溢出问题，提升视觉层级，并将文案优化为标准 SaaS 商业风格。

#### 1\. 布局与容器规范 (Layout Fixes)

  * **网格系统**：使用 CSS Grid 布局，而非 Flexbox 换行，以确保卡片高度强制对齐。
      * **Desktop**: `grid-template-columns: repeat(3, 1fr); gap: 2rem;`
      * **Mobile**: `grid-template-columns: 1fr; gap: 1.5rem;`
  * **防止溢出 (Overflow Protection)**：
      * 所有卡片容器必须设置 `overflow: hidden;`。
      * **最小宽度约束**：设置 `min-width: 280px`，防止在窄屏（如折叠屏手机）下内容被挤压变形。
      * **高度对齐**：卡片必须使用 `display: flex; flex-direction: column;`，并将“立即订阅”按钮设置为 `margin-top: auto`，确保无论内容多少，底部按钮始终对齐。

#### 2\. 文本与排版优化 (Typography & Wrapping)

  * **禁止随意换行**：
      * **价格数字**：必须强制不换行 `white-space: nowrap;`。
      * **标题/短语**：使用 `text-wrap: balance;` 确保标题在两行时视觉平衡，不会出现单字成行。
  * **层级字号规范**：
      * **Plan Name (套餐名)**: `1.25rem (20px)`, Weight 600.
      * **Price (价格)**: `3rem (48px)`, Weight 700, Font `Monospace` (JetBrains Mono).
      * **Unit (单位)**: `/mo` 或 `/year`, `1rem`, color: `var(--text-dim)`.
      * **Feature List (权益)**: `0.875rem (14px)`, `line-height: 1.6`.

#### 3\. 商业文案标准化 (Copywriting Standards)

*请 AI 自动检查并替换非专业文案：*

  * ❌ 拒绝：“买这个”、“很便宜”、“价格是”
  * ✅ **替换为**：
      * **标题**：Basic (基础版) / Pro (专业版) / Enterprise (企业版)
      * **副标题**：适合个人开发者 / 适合小型团队 / 适合大规模商业应用
      * **行动按钮 (CTA)**：Start Free (免费开始) / Upgrade to Pro (升级专业版) / Contact Sales (联系销售)
      * **权益描述**：使用“动词 + 名词”结构，如 "Remove Ads" (移除广告), "Unlimited Export" (无限导出)。

#### 4\. 视觉质感提升 (Visual Polish)

  * **推荐高亮 (Recommended Highlight)**：
      * 针对“Pro”套餐，添加 `border: 2px solid var(--accent-primary);` 和 `transform: scale(1.05)` (Desktop only)。
      * 添加 "Most Popular" 标签：绝对定位在卡片顶部，背景色使用 `var(--accent-primary)`，文字白色。
  * **权益列表图标**：
      * 使用绿色 SVG 对勾图标 (Check icon) `color: var(--state-success)`，严禁使用 Emoji (✅)。


## 5\. 动效编排 (Motion)

*工具类动效必须极快，不能拖泥带水。*

  * **Button Click**: `transform: scale(0.98); transition: 0.1s;` (极速反馈)
  * **Result Reveal**: 结果出现时不要 FadeIn，而是使用 **高度展开 (Expand)** 动画。
      * `height: 0 -> auto; opacity: 0 -> 1; duration: 0.3s; ease: power2.out;`

## 6\. 移动端特殊处理 (Mobile Specifics)

针对 `390px` 宽度的手机：

1.  **隐藏次要元素**: 侧边栏推荐文章、复杂的背景装饰图全部 `display: none`。
2.  **堆叠布局**: 所有左右结构强制变为上下结构。
3.  **触控优化**: 按钮高度至少 `44px`，输入框字体不小于 `16px`。
4.  **Sticky Ads**: 底部保留 `50px` 高度给粘性广告，注意不要遮挡 "提交" 按钮 (需给 body 底部加 `padding-bottom: 50px`)。

-----



### 开发应用示例 (Prompt for AI)

**[如何使用]**:

> "我正在开发一个[Base64转换工具]页面。
> 请基于 `DESIGN_SYSTEM_TOOLING.md` 规范：
>
> 1.  布局：使用 Desktop 基准 (1440px)，左侧是转换工具，右侧预留一个 300x250 的广告位。
> 2.  工具区：上方是多行输入框 (Monospace字体)，中间是'转换'主按钮 (Accent Color)，下方是结果框 (带复制按钮)。
> 3.  移动端适配：小于 768px 时，隐藏右侧广告位，输入框和结果框垂直堆叠。
> 4.  状态：为输入框添加 Focus 时的蓝色光环效果，以及结果生成时的骨架屏加载态。"