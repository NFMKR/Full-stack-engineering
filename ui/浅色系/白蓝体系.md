# VoxScribe Landing Page - UI Design System

## 一、颜色系统 (Color System)

### 1.1 主色调 (Primary Colors)

| 颜色名称 | CSS变量 | HEX值 | RGB | HSL | 应用场景 |
|---------|---------|-------|-----|-----|----------|
| 主色（科技蓝） | `--primary` | `#165dff` | `rgb(22, 93, 255)` | `hsl(222, 100%, 58%)` | 品牌Logo、核心CTA按钮、图标主色、标题高亮、边框聚焦态 |
| 辅助色（浅紫） | `--primary-2` | `#7b61ff` | `rgb(22, 93, 255)` | `hsl(222, 100%, 58%)` | AI模块标识、渐变效果、次要CTA按钮、装饰元素 |
| 背景色 | `--background` | `#f5f7fa` | `rgb(245, 247, 250)` | `hsl(210, 25%, 97%)` | 页面全局背景 |
| 前景色（文本） | `--foreground` | `#0f172a` | `rgb(15, 23, 42)` | `hsl(222, 47%, 11%)` | 主要文本内容 |
| 卡片色 | `--card` | `#ffffff` | `rgb(255, 255, 255)` | `hsl(0, 0%, 100%)` | 功能卡片、表单容器、面板背景 |
| 次要文本 | `--muted` | `#475569` | `rgb(71, 85, 105)` | `hsl(215, 16%, 34%)` | 辅助说明、次要标签 |

### 1.2 Tailwind 语义颜色映射

```css
/* 实际使用的 Slate 色系（来自 Tailwind） */
slate-900: #0f172a  /* 标题文本 */
slate-800: #1e293b  /* 次级标题 */
slate-700: #334155  /* 强调文本 */
slate-600: #475569  /* 描述文本、链接 */
slate-500: #64748b  /* 辅助文本 */
slate-100: #f1f5f9  /* 边框、分隔线 */
slate-50:  #f8fafc  /* 背景高亮、卡片背景 */
```

### 1.3 渐变背景 (Gradient Backgrounds)

```css
/* 页面背景渐变 */
background: 
  radial-gradient(circle at 20% 20%, rgba(230, 237, 255, 1) 0, transparent 25%),
  radial-gradient(circle at 80% 0%, rgba(239, 233, 255, 1) 0, transparent 25%),
  var(--background);

/* Hero区装饰渐变 */
radial-gradient(circle at 10% 20%, rgba(22, 93, 255, 0.1), transparent 25%)
radial-gradient(circle at 80% 0%, rgba(123, 97, 255, 0.12), transparent 20%)

/* Logo/按钮渐变 */
linear-gradient(to bottom right, var(--primary), var(--primary-2))
```

### 1.4 功能色 (Functional Colors)

| 颜色类型 | HEX值 | 应用场景 |
|---------|-------|----------|
| 成功色 | `#00b42a` | 操作成功提示、保存状态 |
| 警告色 | `#ff7d00` | 兼容性提示、异常提醒 |
| 错误色 | `#f53f3f` | 表单验证错误 |
| 绿色指示 | `#10b981` (green-500) | 在线状态、完成标记 |
| 蓝色指示 | `#3b82f6` (blue-500) | 功能说明标记 |
| 琥珀色提示 | `#f59e0b` (amber-700) | 演示/预览标签背景 |

### 1.5 透明度和玻璃态效果

```css
/* 玻璃态卡片 */
background: rgba(255, 255, 255, 0.6);
border: 1px solid rgba(255, 255, 255, 0.5);
backdrop-filter: blur(12px);

/* 导航栏背景 */
background: rgba(255, 255, 255, 0.9);
backdrop-filter: blur(8px);
```

---

## 二、排版系统 (Typography)

### 2.1 字体族 (Font Family)

```css
font-family: var(--font-geist-sans), ui-sans-serif, system-ui, 
             -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
```

- **主字体**: Geist Sans (Next.js 默认)
- **备选字体**: 系统无衬线字体栈
- **等宽字体**: Geist Mono (用于代码/技术展示)

### 2.2 字号与行高 (Font Size & Line Height)

| 文本层级 | Tailwind类 | 桌面端 | 移动端 | 字重 | 应用场景 |
|---------|-----------|--------|--------|------|----------|
| H1 主标题 | `text-4xl md:text-5xl` | 36px / 2.25rem | 32px / 2rem | `font-semibold` (600) | Hero区核心标题 |
| H2 模块标题 | `text-3xl md:text-4xl` | 30px / 1.875rem | 24px / 1.5rem | `font-semibold` (600) | Section标题 (.section-title) |
| H3 卡片标题 | `text-lg` | 18px / 1.125rem | 18px / 1.125rem | `font-semibold` (600) | 卡片标题、功能模块标题 |
| Body 正文 | `text-base` | 16px / 1rem | 16px / 1rem | `font-normal` (400) | 正文描述 |
| Body Small | `text-sm` | 14px / 0.875rem | 14px / 0.875rem | `font-normal` (400) | 辅助文本、按钮文本 |
| Caption | `text-xs` | 12px / 0.75rem | 12px / 0.75rem | `font-medium` (500) | 标签、版权信息 |
| 超小文本 | `text-[10px]` | 10px | 10px | `font-semibold` | 状态标签 |

### 2.3 行高 (Line Height)

- **标题**: `leading-tight` (约 1.2)
- **正文**: 默认 `1.5`
- **按钮**: `1.2`

### 2.4 字重 (Font Weight)

| 字重 | CSS值 | Tailwind类 | 应用场景 |
|------|-------|-----------|----------|
| Regular | 400 | `font-normal` | 正文、描述文本 |
| Medium | 500 | `font-medium` | 标签、次要按钮 |
| SemiBold | 600 | `font-semibold` | 标题、强调文本 |
| Bold | 700 | `font-bold` | 极少使用 |

### 2.5 文本颜色映射

| 文本类型 | Tailwind类 | HEX值 | 应用场景 |
|---------|-----------|-------|----------|
| 标题主色 | `text-slate-900` | `#0f172a` | 主要标题、强调文本 |
| 标题次色 | `text-slate-800` | `#1e293b` | 卡片标题 |
| 正文主色 | `text-slate-700` | `#334155` | 正文内容 |
| 文本次色 | `text-slate-600` | `#475569` | 描述、副标题 (.section-subtitle) |
| 辅助文本 | `text-slate-500` | `#64748b` | 占位符、辅助说明 |
| 链接/强调 | `text-[var(--primary)]` | `#165dff` | 链接、高亮文本 |

---

## 三、布局系统 (Layout System)

### 3.1 容器规范

```css
/* 页面主容器 */
.page-container {
  max-width: 1152px;  /* max-w-6xl */
  margin: 0 auto;
  padding: 0 16px;     /* px-4 */
}
```

| 断点 | 容器宽度 | 左右边距 | 应用场景 |
|------|---------|---------|----------|
| 桌面端 (≥768px) | `1152px` (max-w-6xl) | `16px` (px-4) | 全局页面容器 |
| 移动端 (<768px) | `100%` | `16px` (px-4) | 全局页面容器 |

### 3.2 响应式断点

| 断点名称 | Tailwind前缀 | 宽度范围 | 说明 |
|---------|-------------|---------|------|
| 移动端 | 默认 | < 768px | 手机竖屏 |
| 平板端 | `md:` | ≥ 768px | 平板、手机横屏 |
| 桌面端 | `lg:` | ≥ 1024px | 桌面浏览器 |

### 3.3 模块间距 (Spacing)

```css
/* Section间距 */
.section-gap {
  margin-top: 64px;   /* mt-16 (移动端) */
  margin-top: 80px;   /* md:mt-20 (平板) */
  margin-top: 96px;   /* lg:mt-24 (桌面) */
}
```

| 间距类型 | Tailwind类 | 桌面端 | 平板端 | 移动端 |
|---------|-----------|--------|--------|--------|
| Section间距 | `.section-gap` | 96px (mt-24) | 80px (mt-20) | 64px (mt-16) |
| 卡片间距 | `gap-6` | 24px | 24px | 24px |
| 卡片间距（紧凑） | `gap-4` | 16px | 16px | 16px |
| 按钮间距 | `gap-3` | 12px | 12px | 12px |
| 元素内距 | `p-6` | 24px | 24px | 24px |
| 元素内距（紧凑） | `p-4` | 16px | 16px | 16px |
| 导航栏内距 | `py-3 md:py-4` | 16px | 12px | 12px |

### 3.4 网格布局 (Grid Layout)

```css
/* 桌面端3列 */
grid-cols-3: repeat(3, minmax(0, 1fr))

/* 桌面端2列 */
grid-cols-2: repeat(2, minmax(0, 1fr))

/* Hero区左右分栏 */
grid-cols-[1.1fr_1fr]: 1.1fr 1fr

/* 响应式网格 */
grid gap-6 md:grid-cols-3    /* 移动1列，平板+桌面3列 */
grid gap-6 md:grid-cols-2    /* 移动1列，平板+桌面2列 */
```

---

## 四、组件系统 (Component System)

### 4.1 按钮 (Buttons)

#### 主按钮 (Primary Button)

```css
.btn-primary {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 9999px;        /* rounded-full */
  background: var(--primary);    /* #165dff */
  padding: 12px 20px;            /* px-5 py-3 */
  font-size: 14px;               /* text-sm */
  font-weight: 600;              /* font-semibold */
  color: white;
  box-shadow: 0 4px 6px -1px rgba(59, 130, 246, 0.5);  /* shadow-md shadow-blue-200 */
  transition: all 0.2s;
}

/* Hover态 */
.btn-primary:hover {
  transform: translateY(-2px);   /* -translate-y-0.5 */
  box-shadow: 0 10px 15px -3px rgba(59, 130, 246, 0.6); /* shadow-xl */
}

/* Focus态 */
.btn-primary:focus-visible {
  outline: 2px solid var(--primary);
  outline-offset: 2px;
}
```

**Tailwind类**: `btn-primary`

#### 次按钮 (Secondary Button)

```css
.btn-secondary {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 9999px;
  border: 1px solid #e2e8f0;     /* border-slate-200 */
  padding: 12px 20px;
  font-size: 14px;
  font-weight: 600;
  color: #334155;                 /* text-slate-700 */
  background: transparent;
  transition: all 0.2s;
}

.btn-secondary:hover {
  border-color: var(--primary);
  color: var(--primary);
}
```

**Tailwind类**: `btn-secondary`

### 4.2 卡片 (Cards)

#### 基础卡片

```css
.card {
  border-radius: 16px;           /* rounded-2xl */
  border: 1px solid #f1f5f9;     /* border-slate-100 */
  background: white;
  box-shadow: 0 1px 2px 0 rgba(0, 0, 0, 0.05);  /* shadow-sm */
}
```

#### 悬浮卡片

```css
.card-hover {
  transition: all 0.3s ease-in-out;
}

.card-hover:hover {
  transform: translateY(-4px);   /* -translate-y-1 */
  box-shadow: 0 10px 15px -3px rgba(0, 0, 0, 0.1);  /* shadow-lg */
}
```

**组合使用**: `card card-hover`

### 4.3 玻璃态效果 (Glass Morphism)

```css
.glass {
  background: rgba(255, 255, 255, 0.6);
  border: 1px solid rgba(255, 255, 255, 0.5);
  backdrop-filter: blur(12px);
  -webkit-backdrop-filter: blur(12px);
}
```

**应用**: Demo面板、Hero区装饰卡片


### 4.4 导航栏 (Navigation)

```css
header {
  position: sticky;
  top: 0;
  z-index: 30;
  background: rgba(255, 255, 255, 0.9);
  backdrop-filter: blur(8px);
  border-bottom: 1px solid #f1f5f9;  /* border-slate-100 */
}
```

### 4.5 标题系统 (Typography Utilities)

```css
/* 模块标题 */
.section-title {
  font-size: 30px;                /* text-3xl (移动) */
  font-size: 36px;                /* md:text-4xl (桌面) */
  font-weight: 600;               /* font-semibold */
  color: #0f172a;               /* text-slate-900 */
  letter-spacing: -0.025em;       /* tracking-tight */
}

/* 模块副标题 */
.section-subtitle {
  font-size: 16px;                /* text-base (移动) */
  font-size: 18px;                /* md:text-lg (桌面) */
  color: #475569;               /* text-slate-600 */
  max-width: 768px;               /* max-w-3xl */
}
```

---

## 五、阴影系统 (Shadow System)

| 阴影等级 | Tailwind类 | CSS值 | 应用场景 |
|---------|-----------|-------|----------|
| 微小阴影 | `shadow-sm` | `0 1px 2px 0 rgba(0,0,0,0.05)` | 基础卡片 |
| 小阴影 | `shadow-md` | `0 4px 6px -1px rgba(0,0,0,0.1)` | 按钮、悬浮卡片 |
| 大阴影 | `shadow-lg` | `0 10px 15px -3px rgba(0,0,0,0.1)` | 悬浮卡片、面板 |
| 超大阴影 | `shadow-xl` | `0 20px 25px -5px rgba(0,0,0,0.1)` | Hero区卡片、Demo面板 |
| 彩色阴影 | `shadow-blue-200` | `0 4px 6px -1px rgba(59,130,246,0.5)` | 主按钮 |

---

## 六、圆角系统 (Border Radius)

| 圆角大小 | Tailwind类 | 值 | 应用场景 |
|---------|-----------|-----|----------|
| 小圆角 | `rounded-lg` | `8px` | 输入框、小按钮 |
| 中圆角 | `rounded-xl` | `12px` | 图标容器、标签 |
| 大圆角 | `rounded-2xl` | `16px` | 卡片、面板 |
| 超大圆角 | `rounded-3xl` | `24px` | 大型容器、Section背景 |
| 全圆角 | `rounded-full` | `9999px` | 按钮、徽章、头像 |

---

## 七、动效与交互 (Animations & Interactions)

### 7.1 过渡效果

```css
/* 标准过渡 */
transition: all 0.2s ease-in-out;

/* 悬浮上移 */
hover:-translate-y-1    /* translateY(-4px) */
hover:-translate-y-0.5  /* translateY(-2px) */

/* 点击缩放 */
active:scale-95 
```

### 7.2 平滑滚动

```css
html {
  scroll-behavior: smooth;
}
```

### 7.3 脉冲动画 (Pulse)

```css
animate-pulse {
  animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}
```

**应用**: 在线状态指示器

---

## 八、响应式布局模式 (Responsive Patterns)

### 8.1 Hero区布局

```tsx
// 桌面端: 左右分栏 (60% 文本 + 40% 视觉)
grid md:grid-cols-[1.1fr_1fr]

// 移动端: 上下布局 (文本在上)
flex flex-col md:grid md:grid-cols-[1.1fr_1fr]
```

### 8.2 功能卡片布局

```tsx
// 桌面端3列 → 移动端1列
grid gap-6 md:grid-cols-3

// 桌面端2列 → 移动端1列
grid gap-6 md:grid-cols-2

// 桌面端4列 → 移动端2列
grid gap-6 md:grid-cols-2 lg:grid-cols-4
```

### 8.3 导航栏适配

```tsx
// 桌面端: 完整导航链接
hidden md:flex

// 移动端: 汉堡菜单
md:hidden
```

---

## 九、无障碍设计 (Accessibility)

### 9.1 Focus状态

```css
a:focus-visible,
button:focus-visible,
input:focus-visible {
  outline: 2px solid var(--primary);
  outline-offset: 2px;
}
```

### 9.2 ARIA标签

```tsx
<button aria-label="Start recording">⏺ Start Recording</button>
<button aria-label="Toggle navigation">☰</button>
```

### 9.3 语义化标签

- 使用 `<header>`, `<nav>`, `<main>`, `<section>`, `<footer>`
- 标题层级: `h1` → `h2` → `h3` (不跳过层级)

---

## 十、Tailwind CSS 配置建议

### 10.1 自定义颜色扩展

```javascript
// tailwind.config.js
module.exports = {
  theme: {
    extend: {
      colors: {
        primary: {
          DEFAULT: '#165dff',
          '2': '#7b61ff',
        },
      },
    },
  },
}
```

### 10.2 使用CSS变量

```css
/* 优先使用CSS变量 */
bg-[var(--primary)]
text-[var(--primary)]
border-[var(--primary)]
```

---

## 十一、设计原则总结

1. **极简科技风**: 线性图标、轻渐变、无冗余装饰
2. **一致性**: 同类型组件使用统一样式
3. **响应式优先**: 移动端优先，渐进增强
4. **性能优化**: 使用CSS变换而非布局属性做动效
5. **无障碍**: 保证对比度、键盘导航、语义化标签

---