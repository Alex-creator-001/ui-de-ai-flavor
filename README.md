# ui-de-ai-flavor：UI 设计去 AI 味 Skill

一个给 AI 编码助手（Claude Code / Cursor / Codex 等）使用的 skill。生成、评审、重构前端界面时，让 AI 避开"一眼 AI"的廉价感：颜色过多、字号失控、粗边框、圆角不同心、紫色渐变、装饰堆砌……

内容归纳自 [Bruce Van 推荐的 8 位中文设计师](https://x.com/bruc3van/status/2115963644811116732) 的公开推文。

## 目录
```
SKILL.md                    # 主 skill：原则、检查清单、工作流、prompt 片段
references/designers.md     # 8 位设计师要点与来源链接
references/slop-checklist.md# AI slop 黑名单 + 量化阈值
references/css-snippets.md  # 嵌套圆角、superellipse、0.5px、Radix Colors、中文字体栈
examples/before-after.html  # 去 AI 味前后对比
```

## 安装
- **Claude Code**：`git clone <本仓库> ~/.claude/skills/ui-de-ai-flavor`（或放到项目的 `.claude/skills/`）。
- **Cursor**：克隆到项目 `.cursor/skills/ui-de-ai-flavor`，或把 `SKILL.md` 内容加入 Rules。
- **其他工具**：把 `SKILL.md` 作为系统提示/项目规则，`references/` 按需附带。

## 使用
- 让 AI 做界面时说："用 ui-de-ai-flavor 做这个页面"。
- 评审已有界面："按 ui-de-ai-flavor 的 slop-checklist 审查这个页面，只修最严重的一项"。
- 也可以直接复制 `SKILL.md` 末尾的 prompt 片段。
- 打开 `examples/before-after.html` 看对比效果。

## 来源与致谢
- 推荐清单：Bruce Van [@bruc3van](https://x.com/bruc3van/status/2115963644811116732)
- [@Kubai087 枯白啃设计](https://x.com/Kubai087/status/2115469767650021796) — 递进式圆角与超椭圆
- [@ZaynHao](https://x.com/ZaynHao/status/2113456751915982917) — 10 条界面优化提示词（[配色补充](https://x.com/ZaynHao/status/2111685618925474098)）
- [@ianneo_ai 伊恩](https://x.com/ianneo_ai/status/2115277214149451968) — 只用黑白灰，颜色留给内容
- [@dingyi](https://x.com/dingyi/status/2115790005423734818) — AI slop 特征清单
- [@Xian0063 弦](https://x.com/Xian0063/status/2114306504778256445) — 8 条审美原则 + 5 个 AI 设计 Skill
- [@yanliudreamer](https://x.com/yanliudreamer/status/2113188741452103685) — 10 个 UI 组件工具库
- [@ricouii](https://x.com/ricouii/status/2113462025556996412) — 中文网页 font-family
- [@remixdesigner](https://x.com/remixdesigner/status/2100082157184229741) — Preview 图标 Clear 模式单独图层

## 免责声明
本仓库内容是对上述公开推文的归纳与转述，并非逐字复制；观点与原始内容版权归原作者所有。如有不当，请提 issue，我们会及时修改或移除。代码片段与示例为本仓库自行编写，按 MIT 协议发布。
