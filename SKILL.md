---
name: ui-de-ai-flavor
description: 去除前端界面的 "AI 味"/廉价感。在生成、评审或重构前端界面（网页、App、Dashboard、落地页、vibe coding 产出的 UI）时使用；当用户说界面"一眼 AI""廉价""不精致""没质感""去 AI 味"，或要求按设计规范打磨 UI 时触发。
---

# UI 去 AI 味（ui-de-ai-flavor）

vibe 出来的界面显得廉价，通常不是布局大错，而是一堆细节同时失守：颜色太多、字号太多、边框太粗、圆角不同心、到处是装饰。本 skill 把 8 位中文设计师公开分享的经验（见 `references/`）整理成可执行规则。

## 核心原则

1. **克制优先**：每加一个元素/颜色/阴影/动效都要有功能理由，否则删掉。
2. **界面让位于内容**：UI 外壳只用黑白灰（中性色阶），颜色留给照片、数据、状态和唯一的主操作。
3. **一致的系统**：颜色、字号、间距、圆角、边框都来自少量 token，不硬编码随手值。
4. **几何正确**：嵌套圆角同心，光学对齐，4px 网格。
5. **文案干净**：不写解释性废话，不造词，不用 `·` 分隔，不塞 emoji。
6. **先定义再生成，先全貌再逐块改**：每轮只改一处。

## 可执行检查清单

### 圆角
- 嵌套公式：`inner = outer - padding`（r = R − p），内外共用圆心；从外向内逐层计算。例：dialog 32 / padding 16 → 内部面板与按钮 16；16 的面板里 padding 8 的 chip → 8。
- 同层级元素同一圆角；最小不低于 4px；pill/圆形保持全圆。
- 连续圆角（类 iOS squircle）作为渐进增强：`@supports (corner-shape: superellipse(1.25))`，不支持的浏览器自动回退普通 `border-radius`。
- 不要给所有东西随手加圆角，按功能场景定值。

### 边框与线条
- 需要线条/边框时用 **0.5px**（hairline），全站粗细统一；禁止 1px 粗边框到处用。
- 能用间距、背景明度差分区的，就不要用分割线和带边框容器。
- 禁止卡片左边缘的彩色竖线。

### 字号层级
- 全页字号 **≤ 4 种，最好 3 种**；最小 12px。
- 层级不够时用字重、颜色（灰阶）、间距区分，不要再加字号。
- hero 标题别大到离谱；禁止全大写小标题、标题上方小眉标（eyebrow）、章节编号。

### 配色
- 外壳只用中性灰阶（如 Radix `gray`/`slate`/`sand` 的 1–12 级），只选 1 个强调色，品牌色总计 3–5 个以内。
- 统一使用 Radix Colors 的 12 级语义：1–2 背景，3–5 组件底色（常态/hover/按下），6–8 边框，9–10 实色填充，11–12 文字。
- 禁止：紫色/紫蓝渐变、渐变按钮、彩色图标、一张卡片一种颜色、半透明叠色堆叠、多层阴影。

### 字体
- 避开被用烂的 slop 字体：Instrument Serif、Space Grotesk、Bricolage Grotesque；不滥用等宽字体（只给代码/数字表格）。
- 中文 `font-family`：**先西后中**，中文字体写英文名，带空格的名字加引号，最后 `sans-serif` 兜底（完整栈见 `references/css-snippets.md`）。
- 斜体与标签（tag/badge）不要到处用。

### 图标
- 一套图标库、同一线宽、同一填充风格、同一视觉重量（例如统一用 Remix Icon 或 Lucide，不混搭）。
- 去掉标题前的装饰 emoji/图标；下拉按钮不要多余的下拉小箭头图标堆叠。
- 浅色/透明/深色等不同模式下，图标需要单独适配，而不是直接滤镜转换。

### 间距与对齐
- 所有 padding / gap / radius 落在 4px 网格。
- 光学对齐（图标、圆形、文字基线），而非仅几何对齐。
- 避免卡片套卡片、全部居中排版。

### 动效
- 能少则少；需要时进场用 `ease-out`，约 200–250ms；不用 `ease-in` 做进场。
- 弹出层从触发点缩放（从 0.96 而非 0）；按钮按下 `scale(0.97)`。
- 禁止滚动触发的一堆动画。

### 文案
- 删除解释性描述文本；不用 `·` 作分隔符；不造词、不过度口语化；正文不塞 emoji；不编造数据（如 "10,000+ 满意客户"）。

完整黑名单见 `references/slop-checklist.md`。

## 工作流

### 生成前（定义）
1. 写清：给谁用、解决什么问题、想要什么感觉。说不清就先向用户提问，不出设计。
2. 定 token：中性色阶 + 1 个强调色（Radix）、3–4 级字号、4px 间距梯度、圆角梯度（外层 R，内层按公式推导）、0.5px 边框、字体栈。
3. 选库：一个组件库/图标库，不混搭。

### 生成中
- 只用 token，不硬编码随手值；嵌套容器按 `R - p` 算圆角。
- 默认无阴影、无渐变、无装饰线；需要时逐个论证。
- 先出完整页面，再逐块改。

### 生成后（自查评审）
1. 对照 `references/slop-checklist.md` 逐条打勾，列出命中项。
2. 统计：颜色数（不含灰阶）、字号种类、边框宽度种类、圆角值种类、阴影种类、动画数量。超标即修。
3. 按严重程度排序问题，每轮只修一处，修完截图复查（建议 375 / 768 / 1440 三种宽度）。
4. 输出变更清单：`element: old -> new`。

## 可直接复制给 AI 的 prompt 片段

**总纲**
```
Remove the "AI-generated" look from this UI. Use only neutral grays for the chrome (backgrounds, cards, inputs, buttons); reserve color for content, data and the single primary action. Max 4 font sizes (prefer 3), min 12px; build hierarchy with weight, gray shade and spacing instead. Borders/dividers are 0.5px and consistent. No gradients, no purple, no multi-layer shadows, no colored left-border on cards, no all-caps eyebrows, no emoji in text, no "·" separators, no explanatory filler copy. Keep all spacing and radii on a 4px grid. List every change as "element: old -> new".
```

**圆角**
```
Make corner radii consistent: inner radius = outer radius - padding (r = R - p), working from the outside in. Same-level boxes share one radius; never below 4px; pills/circles stay fully round. Add continuous corners as progressive enhancement: @supports (corner-shape: superellipse(1.25)) { :where(*) { corner-shape: superellipse(1.25); } } and corner-shape: round on pills. Use radius tokens if the project has them.
```

**配色**
```
Replace every color with Radix Colors scales (e.g. slate for neutrals + one accent). Follow the 12-step usage: 1-2 app/subtle backgrounds, 3-5 component backgrounds (normal/hover/active), 6-8 borders, 9-10 solid fills, 11-12 text.
```

**中文字体**
```
Set font-family as Latin fonts first, then Chinese fonts by English names, quoted if they contain spaces, ending with sans-serif. Use the --font-sans / --font-mono stacks from css-snippets.md. Do not use Instrument Serif, Space Grotesk or Bricolage Grotesque.
```

**评审**
```
Audit this page against slop-checklist.md. For each hit, give: rule, element, evidence, fix. Then fix only the top issue and stop for review.
```

## 参考
- `references/designers.md` — 8 位设计师要点与来源
- `references/slop-checklist.md` — AI slop 黑名单
- `references/css-snippets.md` — 可直接用的 CSS
- `examples/before-after.html` — 前后对比示例
