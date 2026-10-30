# CSS 片段

## 1. 嵌套圆角（r = R − p）
```css
.card {
  --r: 24px;
  --p: 8px;
  border-radius: var(--r);
  padding: var(--p);
}
.card > .inner {
  /* 不低于 4px */
  border-radius: max(4px, calc(var(--r) - var(--p)));
}
```
多层嵌套时把子层也声明为新的 `--r`：
```css
.card > .inner { --r: max(4px, calc(24px - 8px)); --p: 8px; border-radius: var(--r); padding: var(--p); }
```

## 2. 连续圆角（superellipse，渐进增强）
来源：@Kubai087。`corner-shape` 目前仅 Chromium 139+ 支持，其他浏览器忽略整块并使用普通 `border-radius`。
```css
.surface { border-radius: 32px; }

@supports (corner-shape: superellipse(1.25)) {
  :where(*) { corner-shape: superellipse(1.25); }
  .pill, .avatar { corner-shape: round; }
}
```
不支持 `corner-shape` 时的备选：用 SVG/`clip-path: path()` 绘制 squircle（固定尺寸场景），或接受普通圆角回退。

## 3. 0.5px 发丝边框
```css
:root { --hairline: 0.5px; --border: var(--gray-6, rgba(0,0,0,.12)); }
.box { border: var(--hairline) solid var(--border); }

/* 1x 屏上 0.5px 可能被取整为 0 或 1px，可退回 1px 并降低对比度 */
@media (max-resolution: 1dppx) {
  :root { --hairline: 1px; --border: rgba(0,0,0,.08); }
}

/* 或用 inset box-shadow 模拟，不影响布局 */
.box-alt { box-shadow: inset 0 0 0 0.5px var(--border); }
```

## 4. Radix Colors
```bash
npm i @radix-ui/colors
```
```css
@import "@radix-ui/colors/slate.css";
@import "@radix-ui/colors/slate-dark.css";
@import "@radix-ui/colors/blue.css";
@import "@radix-ui/colors/blue-dark.css";

/* 1-2 背景 | 3-5 组件底色 | 6-8 边框 | 9-10 实色 | 11-12 文字 */
body    { background: var(--slate-1); color: var(--slate-12); }
.panel  { background: var(--slate-2); border: 0.5px solid var(--slate-6); }
.button { background: var(--slate-3); color: var(--slate-12); }
.button:hover  { background: var(--slate-4); }
.button:active { background: var(--slate-5); }
.muted  { color: var(--slate-11); }
.primary { background: var(--blue-9); color: #fff; }
.primary:hover { background: var(--blue-10); }
```
深色主题文件在 `.dark` / `.dark-theme` 类下生效（给根元素加 `class="dark"`）。

## 5. 中文字体栈（来源：@ricouii）
```css
:root {
  --font-sans: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
    "Helvetica Neue", Helvetica, Arial,
    "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei UI", "Microsoft YaHei",
    "Noto Sans CJK SC", "Noto Sans SC", "Source Han Sans CN", sans-serif;
  --font-mono: "JetBrains Mono", "SF Mono", ui-monospace, Menlo, Consolas,
    "Liberation Mono", "Courier New", monospace;
}
body { font-family: var(--font-sans); }
code, pre, kbd { font-family: var(--font-mono); }
```
注意：原推中代码示例写作 `var(-font-mono)`，正确写法是 `var(--font-mono)`（两个连字符）。

## 6. 字号与间距 token
```css
:root {
  --text-sm: 12px; --text-md: 14px; --text-lg: 20px; --text-xl: 32px; /* 最多 4 级 */
  --space-1: 4px; --space-2: 8px; --space-3: 12px; --space-4: 16px; --space-6: 24px; --space-8: 32px;
}
```

## 7. 克制的动效
```css
.popover {
  transform-origin: var(--origin, top left);
  animation: pop-in 200ms cubic-bezier(0.16, 1, 0.3, 1);
}
@keyframes pop-in { from { opacity: 0; transform: scale(0.96); } }
.button:active { transform: scale(0.97); }
@media (prefers-reduced-motion: reduce) { * { animation: none !important; transition: none !important; } }
```
