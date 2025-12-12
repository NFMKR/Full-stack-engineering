**面向 AI 的原子化设计系统构建指南**。

-----

# AI 辅助开发专用设计系统指南 (`DESIGN_SYSTEM.md`)

**[使用说明]**：
在开始任何开发对话前，请将以下内容投喂给 AI，并附加指令：

> “你现在是本项目的主理前端架构师。请严格遵循以下 `DESIGN_SYSTEM.md` 中的视觉规范、代码风格和组件原子进行开发。严禁引入规范之外的颜色、字体或‘魔法数值’。如果遇到未定义的情况，请优先推导最接近的规范变量。”

-----

## 1\. 全局设计原则 (The Axioms)

  * **设计哲学**：[此处填入，例如：工业极简、深邃黑石、秩序之美]
  * **核心约束**：
      * **No Magic Numbers**：禁止在 CSS 中直接写 `13px`, `#333` 等硬编码数值。必须使用 CSS 变量。
      * **Mobile First**：优先编写移动端样式，使用 `@media (min-width)` 覆盖桌面端。
      * **语义化 HTML**：布局必须使用 `<section>`, `<article>`, `<nav>` 等标签，而非全部 `<div>`。

## 2\. 设计令牌 (Design Tokens - Source of Truth)

AI 必须直接复用这些 CSS 变量，而不是重新发明颜色。

```css
/* 复制此块到你的全局 CSS 文件 (global.css) */
:root {
  /* --- 1. 色彩体系 (Colors) --- */
  /* 背景层级：从深到浅 */
  --bg-app:        #050505; /* 应用底色 */
  --bg-surface:    #0F1115; /* 卡片/模块背景 */
  --bg-elevated:   #1A1D24; /* 悬浮层/弹窗 */
  
  /* 品牌色 (Brand) */
  --brand-primary: #2E5CFF; /* 主行动点 */
  --brand-glow:    #00F0FF; /* 光晕/高亮 */
  
  /* 文本色 (Text) - 使用透明度实现层级 */
  --text-primary:  rgba(255, 255, 255, 0.95);
  --text-secondary:rgba(255, 255, 255, 0.70);
  --text-tertiary: rgba(255, 255, 255, 0.40);
  
  /* 边框与分割 (Borders) */
  --border-dim:    rgba(255, 255, 255, 0.05);
  --border-light:  rgba(255, 255, 255, 0.15);

  /* --- 2. 空间体系 (Spacing) --- */
  /* 基于 4px 网格系统 */
  --space-xs:  4px;
  --space-sm:  8px;
  --space-md:  16px;
  --space-lg:  32px;
  --space-xl:  64px;
  --space-2xl: 120px; /* 板块间距 */
  
  /* --- 3. 排版体系 (Typography) --- */
  --font-sans: 'Inter', system-ui, -apple-system, sans-serif;
  
  /* 响应式字体大小 (Clamp) */
  --text-display: clamp(3rem, 5vw, 5rem);  /* 巨型标题 */
  --text-h1:      clamp(2rem, 3vw, 3rem);  /* 一级标题 */
  --text-h2:      clamp(1.5rem, 2vw, 2rem);/* 二级标题 */
  --text-body:    1rem;                    /* 正文 */
  --text-sm:      0.875rem;                /* 说明文 */

  /* --- 4. 质感与特效 (Effects) --- */
  --radius-sm: 4px;   /* 工业硬朗感 */
  --radius-md: 8px;
  --radius-full: 999px;

  --glass-surface: blur(12px);
  --shadow-glow: 0 0 20px rgba(46, 92, 255, 0.3);
}
```

## 3\. 原子组件规范 (Atomic Patterns)

要求 AI 在生成具体组件时，必须符合以下结构模式。

### A. 按钮 (Buttons)

  * **规则**：按钮不应只有背景色，要有微交互和光影。
  * **通用 CSS 类名模式**：`.btn`, `.btn-primary`, `.btn-ghost`
  * **代码范式**：
    ```css
    .btn {
      padding: var(--space-sm) var(--space-lg);
      border-radius: var(--radius-sm);
      font-weight: 600;
      transition: all 0.3s ease;
      cursor: pointer;
    }
    .btn-primary {
      background: var(--brand-primary);
      color: #FFF;
      /* Hover 效果：必须是发光而非简单的变色 */
    }
    .btn-primary:hover {
      box-shadow: var(--shadow-glow);
      transform: translateY(-2px);
    }
    ```

### B. 卡片 (Cards)

  * **规则**：所有卡片必须使用“玻璃拟态”或“微边框”，禁止使用纯色不透明背景。
  * **代码范式**：
    ```css
    .card {
      background: rgba(255, 255, 255, 0.03);
      border: 1px solid var(--border-dim);
      backdrop-filter: var(--glass-surface);
      padding: var(--space-lg);
    }
    ```

### C. 布局容器 (Container)

  * **规则**：页面内容必须包裹在 Container 中，且必须有最大宽度。
  * **范式**：
    ```css
    .container {
      width: 100%;
      max-width: 1280px;
      margin: 0 auto;
      padding-inline: var(--space-md);
    }
    ```

## 4\. 交互与动效规范 (Motion Guide)

AI 通常会忽略动效，必须强制要求它添加。

  * **滚动库**：必须集成 `Lenis`。
  * **动画引擎**：必须使用 `GSAP` (`ScrollTrigger`)。
  * **标准动画参数**：
      * **进入 (Fade Up)**：`y: 30` -\> `0`, `opacity: 0` -\> `1`, `duration: 0.8s`, `ease: "power2.out"`
      * **交错 (Stagger)**：列表元素之间必须有 `0.1s` 的 stagger。
  * **Hover 物理**：所有可交互元素在 hover 时必须有物理反馈（位移、缩放或光标变化）。

## 5\. 负面提示 (Negative Constraints)

明确告诉 AI **绝对不要做**的事情：

1.  **禁止**使用纯黑 (`#000`) 作为背景，这会看起来像网页没加载完。始终使用 `var(--bg-app)`。
2.  **禁止**使用系统默认字体栈作为首选，必须引入 Google Fonts (Inter/Roboto)。
3.  **禁止**使用复杂的 `box-shadow` 黑色投影，深色模式下应使用“发光”或“边框高亮”来区分层级。
4.  **禁止**生成超过 3 层嵌套的 CSS 选择器（保持 CSS 扁平化）。
5.  **禁止**在 JavaScript 中操作样式（`style.color = ...`），必须通过切换 class (`classList.add`) 来改变状态。

-----

### 如何使用这份指南？

1.  **项目初始化时**：把上面的 CSS `root` 变量块直接发给 AI，让它帮你生成 `style.css` 基础文件。
2.  **生成页面时**：
      * *错误提示*：“帮我写一个产品介绍部分。”
      * *正确提示*：“基于 `DESIGN_SYSTEM.md`，使用 `<section>` 标签开发一个‘产品特性’板块。背景使用 `bg-surface`，包含 3 个并排的 `.card`，每个卡片内有图标和文本。**要求卡片使用玻璃拟态，并且配置 GSAP 的 ScrollTrigger 入场动画**。”
3.  **Code Review 时**：
      * 如果 AI 生成了 `#333`，直接斥责：“违反设计系统，请将硬编码颜色替换为 `var(--bg-surface)`。”

这套体系的核心在于**将“审美”抽象为“变量”**。只要 AI 遵守变量，无论它怎么写布局，出来的东西味道都是对的。