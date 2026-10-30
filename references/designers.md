# 8 位设计师要点（归纳转述）

> 由 Bruce Van（@bruc3van）的推文 https://x.com/bruc3van/status/2115963644811116732 推荐。以下为对公开推文的转述，版权归原作者。

## 1. @Kubai087 枯白啃设计 — 递进式圆角 + 超椭圆
来源：https://x.com/Kubai087/status/2115469767650021796 （《999 个小技巧，让你 Vibe 的产品更有质感》004；该推为编辑版，早期版本 https://x.com/Kubai087/status/2115461268723360073）
- 嵌套元素"等距内缩"：内圆角 = 外圆角 − 间距，内外共用一个圆心。
- 由外到内逐层推导（对话框/卡片 → 面板、输入框、按钮 → chip/tag）；同层同值；最小 4px；pill 与圆保持全圆。
- padding、gap、radius 都放在 4px 网格。
- 连续圆角：保留 `border-radius`，用 `@supports` 加 `corner-shape: superellipse(1.25)` 做渐进增强；作者注明 Chrome/Edge 139+ 支持，Safari/Firefox 回退普通圆角。
- 配套英文 Prompt 要求 AI 优先改 radius token，并输出 `element: old -> new` 清单。
- 补充（评论区 @MrWillCom 转推）：superellipse 参数会影响视觉上匹配的半径，不支持时尺寸可能偏差，可用 mixin 计算 fallback 半径。

## 2. @ZaynHao — 10 条优化界面的提示词
来源：https://x.com/ZaynHao/status/2113456751915982917 ；配色补充 https://x.com/ZaynHao/status/2111685618925474098
- 不用 `·` 作分隔符；删除冗余解释性文本。
- 文案贴合目标人群，不过度口语化，不造词。
- 全部颜色换成 Radix UI Colors，并遵循其使用规范（12 级色阶按场景分组）。
- 光学对齐；嵌套处同心圆角。
- 线条/边框用 0.5px。
- 少用动效；需要时 ease-out、250ms 起步。
- 字号不超过 4 种（最好 3 种），最小 12px；层级靠字重、颜色、间距。
- 减少需要用户判断的交互；重新梳理信息优先级。
- 不随意用圆角、阴影，尤其不要卡片左侧彩色竖线。
- 配色补充：选 3–5 个有特点的颜色，可从喜欢的产品中提取基调（如偏暖的米白背景）。

## 3. @ianneo_ai 伊恩 — 颜色给多了就廉价
来源：https://x.com/ianneo_ai/status/2115277214149451968
- 以一个优秀旅行类界面为例：按钮、卡片、输入框基本是白和灰，颜色都在照片里。
- AI 常见问题：渐变按钮、彩色图标、一卡一色，元素都想抢眼，结果廉价。
- 细节：随内容情境（夜晚行程）整体变暗，而不是生硬切换深色模式。
- 给 AI 的一句话：界面只用黑白灰，颜色留给照片和内容。

## 4. @dingyi — AI slop 特征清单
来源：https://x.com/dingyi/status/2115790005423734818
- 全部条目已整理进 `slop-checklist.md`。要点：三大 slop 字体（Instrument Serif、Space Grotesk、Bricolage Grotesque）、紫色渐变、全大写小标题、中圆点分隔、细节过度（分割线、多层阴影、半透明叠色、带边框容器）、0.5px 该用却用 1px、字号超 4 种、卡片左侧彩色竖线、多余的下拉小图标（作者认为最严重）。

## 5. @Xian0063 弦 — 设计审美心得（1）：8 条原则 + 5 个 AI 设计 Skill
来源：https://x.com/Xian0063/status/2114306504778256445 （X 长文）
- AI 页面典型特征：紫蓝渐变、居中排版、卡片套卡片、标题上顶 emoji 图标。
- 推荐 Skill：UI UX Pro Max（按行业出设计系统）、Taste Skill（先定方向求原创，多宽度截图自查）、Impeccable（命令式逐块修，内置 AI 味检测规则）、Emil Kowalski Skills（动效与细节：ease-out 进场、下拉从 0.96 缩放、按下 0.97、长文本截断）、Hallmark（sloplint 分级检查，拦截编造数据、英文小标签等）。
- 8 条原则（转述）：从好作品和日常痛点找需求；先定义再动手；拆解原理不照搬画面；用目标给反馈、数值交给 AI；先出全貌再逐块改、每轮一处；先统一视觉规则；先上线再优化；按反馈分配精力。

## 6. @yanliudreamer — 10 个 UI 组件/工具库
来源：https://x.com/yanliudreamer/status/2113188741452103685 （X 长文《审美提升(下)》）
- Coolors（配色探索，锁定主色生成辅助色）、Fontshare（免费高质量字体）、The Noun Project（图标，注意线宽/重量统一）、Blush（可组合插画）、React Bits（动效组件）、Spline（3D）、Unsplash（图片）、CTA Gallery（按钮案例）、Frontify（品牌规范）、The Shape of AI（AI UX 模式）。
- 观点：精致感常藏在图标线条、圆角、比例是否统一；同一产品用同一风格体系。

## 7. @ricouii — 中文网页 font-family
来源：https://x.com/ricouii/status/2113462025556996412
- 原则：先西后中、兼顾主流系统、最后 `sans-serif` 兜底；代码用独立 mono 栈。
- 避坑：西文必须在中文前（否则中文字体自带英文字形覆盖）；中文字体写英文名；名称含空格加双引号；不声明字体时浏览器默认字体不一定是系统字体。
- 完整栈见 `css-snippets.md`。

## 8. @remixdesigner（Remix Icon 作者）— 图标细节
来源：https://x.com/remixdesigner/status/2100082157184229741
- 观察苹果新版 Preview 图标：为 Clear（透明）模式单独做了图层，推测是因为直接把默认模式图转换会显得脏。
- 启示：图标在不同外观模式（默认/深色/透明/着色）下应单独设计适配，而不是靠滤镜或透明度一键转换。
