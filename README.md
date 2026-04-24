# AI Agent Slidev Deck Handoff

这个项目是一个用于内部分享的 Slidev 课程 deck，主题是 AI Agent 的基本原理、产品形态、能力扩展层和工程演进。

目标不是做一份泛泛的大纲，而是做一套可以讲给非计算机专业同事听的课程讲义。听众可以理解一点编程概念，例如会 C 语言，但不要默认他们懂复杂系统工程术语。

## 当前核心方向

这套课的主线已经确定：

1. 先讲 `LLM` 的基本机制和限制。
2. 再解释为什么仅靠 chatbot 不够，为什么需要 agent。
3. 强调 agent 不是模型本身，而是承载模型的软件系统。
4. 讲清楚 agent 为什么比早期 chatbot 强很多：关键是 `Agent Runtime（Agent 运行层）`、`Tool Use（工具调用）`、状态管理和反馈闭环；这里的 runtime 不是泛指 OS / Node.js / 浏览器运行时，而是 agent 应用内部驱动 “模型 -> 动作 -> 观察 -> 再行动” 的运行层。`Shell Access（命令行执行）` 是一种很强的执行类工具，不要讲成 Runtime 本身。
5. 单独开一章介绍市面上常见的 agent 产品，重点会逐渐转向 `Codex`，后续计划在这里插入视频展示 Codex 能力。
6. 讲 agent 的能力扩展层：Tools、RAG、MCP、Skills、Memory、Subagents。
7. 最后讲 `Prompt Engineering -> Context Engineering -> Harness Engineering` 的演进原因。

用户特别强调：

- 不要把 `agent` 过度讲成 `coding agent`。Codex 也可以做代码之外的任务。
- 观点句用中文即可，不要中英重复同一句废话。
- 专业术语可以保留英文，但第一次出现要补中文解释。
- 不要自造概念，尽量用业界已有术语，例如 `ReAct`、`Runtime`、`Harness`、`MCP`、`Skill`。
- 注意术语边界：`Runtime` 在通用软件里可以指 OS、语言、浏览器等运行时；本 deck 讲 agent 能力边界时，应具体说 `Agent Runtime / Agent 运行层`。`Harness` 是围绕 agent 的任务约束、上下文组织、工具配置、验证和协作设计。两者相关，但不能混成同义词。
- 内容要像教案，不要像提纲。要让同事真的能理解并上手。

## 当前文件结构

入口文件：

- `slides.md`

章节文件：

- `slides/01-llm-why-agent.md`
- `slides/02-products-and-usage.md`
- `slides/03-capability-stack.md`
- `slides/04-engineering-evolution.md`

全局样式：

- `styles/index.css`

课程目录索引：

- `course-outline/README.md`

配图规划：

- `public/generated-images/image-plan.md`

产品截图：

- `public/products/claude-code.webp`
- `public/products/codex.webp`
- `public/products/cursor.webp`
- `public/products/openclaw-chatbot.png`
- `public/products/openclaw-web.avif`
- `public/products/n8n.png`

旧 SVG 图：

- `public/generated-images/*.svg`

这些旧 SVG 图用户明确不喜欢，当前不要继续往 slide 里引用。后续应使用 GPT image 生成中文讲解图，再嵌入 deck。

## 当前章节状态

### `slides.md`

包含：

- 封面页
- chatbot / agent / workflow 对比页
- 课程路线页
- `src` 导入四个章节文件

注意：

- 之前封面页里放过产品截图拼图，用户认为产品介绍不应该掺在第一张 agent 介绍里。
- 现在封面只讲 agent 课程主题，产品章节已经单独放到 `slides/02-products-and-usage.md`。

### `slides/01-llm-why-agent.md`

包含：

- 章节页：先讲 LLM 为什么不够
- `LLM` 的 `next-token prediction`
- 为什么“词语接龙”机制已经很强
- 最早 chatbot 的天花板
- 为什么我们需要 agent
- Agent 是什么，不是什么
- Agent 和 LLM 的关系
- `ReAct`
- Agent 为什么比最早的 chatbot 强很多
- `Shell Access` 为什么扩大能力边界

重要已修复问题：

- 文件末尾曾经残留一个单独的 `---`，导致第 14 页空白。
- 这个残留分隔线已经删除。

### `slides/02-products-and-usage.md`

现在是独立产品章节，开头新增了章节页：

- 市面上常见的 Agent 产品

包含：

- 常见 agent 产品形态
- 不同产品背后的共同 agent 内核
- Claude Code 特点与边界
- Codex 特点与边界
- 使用 Claude Code / Codex 的 6 条规则
- 第一次把任务交给 agent 工具的模板
- Claude Code / Codex / Cursor 选择建议
- 什么是适合交给 agent 的任务
- 新手常见错误

后续重点：

- 用户想重点介绍 `Codex`。
- 这里后续需要预留或新增视频展示页，用于放 Codex 能力演示。

### `slides/03-capability-stack.md`

包含：

- Agent capability stack
- Tools
- MCP 是什么
- MCP 三原语
- 一个 MCP server 在真实工作里长什么样
- 什么时候值得接 MCP server
- Skill 是什么
- Skill / Prompt / Tool / Memory 区别
- 一个 Skill 在真实工作里长什么样
- 什么时候该把 prompt 升级成 skill
- Memory
- 没有 Memory 会怎样
- Subagents
- 复杂任务如何拆给多个 Subagents
- 能力组合总结
- 优先补哪 4 层能力

用户希望这部分继续补细：

- `MCP` 可以单独讲几页。
- `Skill` 也可以单独讲几页。
- 需要更像教学，不要只给结论卡片。

### `slides/04-engineering-evolution.md`

包含：

- 为什么最早是 `Prompt Engineering`
- 为什么演进到 `Context Engineering`
- 为什么 `Context Engineering` 不够
- `Harness Engineering`
- `Prompt -> Context -> Harness` 演进逻辑
- Agent 发展历程
- 什么时候该用 Agent
- 总结
- 参考资料

用户之前认为这条线最需要讲清楚“为什么会演进”，不要只写三个名词。

## 样式与排版状态

当前样式整体偏 Claude 风格：

- 暖色纸张背景
- serif 大标题
- terracotta / warm orange 作为强调色
- ivory 卡片
- section-dark 章节页

样式文件：

- `styles/index.css`

已经做过的修复：

- 修掉了 inline `code` 黑底黑字问题。
- 调整了全局标题、卡片 padding、列表间距，减少溢出。
- 给长标题页增加了 `title-compact` 和 `page-tight`。
- 给规则页增加了 `rule-mosaic`、`rule-card`。
- 给工具页增加了 `tools-three`。
- 将 section 页从过度居中改成偏上布局，减少空白感。

仍需注意：

- 新增内容时要检查高度，不要让卡片写到页面外。
- 不要每页都堆白色卡片，用户要求排版灵活。
- 图片页、定义页、表格页、对比页应该使用不同布局。
- 不要再加入看起来像空白页的孤立 `---`。

## 空白页问题的已知原因

之前出现空白页主要有两个原因：

1. 某些页面前面多写了：

```md
---

---
class: ...
---
```

这会被 Slidev 解释成一张真正的空白页。

2. 某个章节文件末尾残留了一个单独的 `---`。

这个会导致章节末尾多出一张空 slide。

后续编辑时，遇到空白页优先检查：

```bash
rg -n '^---$' slides.md slides
tail -n 20 slides/*.md
```

## 图像策略

用户明确不喜欢旧 SVG 图。后续应使用 GPT image 生成中文讲解图。

图片使用原则：

- 定义、判断、边界页：文字排版为主。
- 机制、流程、结构页：图文结合或整页图。
- 产品形态页：优先使用真实产品截图。
- 复杂能力页：用图建立直觉，再用文字讲边界和例子。

目前配图计划已写在：

- `public/generated-images/image-plan.md`

优先生成 5 张图：

1. `LLM 的基本机制：next-token prediction`
2. `ReAct / agent loop`
3. `MCP 的 3 个原语`
4. `Skill 是什么`
5. `Prompt -> Context -> Harness` 演进图

注意：

- 图片中文字要用中文。
- 图要帮助理解关系、流程、结构，不要为了装饰而放图。
- 图像风格可以不完全匹配 PPT，但必须讲清楚。

## Image generation rule

GPT image 工具默认会先把生成图保存到：

- `/Users/kay/.codex/generated_images/...`

这个目录只当作临时输出区，不要在 Slidev deck 里直接引用它。

正式用于课程的图片必须先复制到项目目录：

- `public/generated-images/`

Slidev 中只引用项目内路径，例如：

```md
<img src="/generated-images/llm-next-token.png" />
```

推荐命名方式：

- `llm-next-token.png`
- `react-agent-loop.png`
- `mcp-primitives.png`
- `skill-pack.png`
- `prompt-context-harness.png`

后续生成图片时的固定流程：

1. 使用 GPT image 生成候选图。
2. 从 `/Users/kay/.codex/generated_images/...` 里选择最终版本。
3. 复制到 `public/generated-images/`。
4. 只在 slide 中引用 `/generated-images/...`。
5. 原始生成图可以留在 `.codex/generated_images`，不需要删除。

视觉协作约定：

- 用户会作为 human reviewer 审核图片效果。生成或替换图片后，不要每次都主动截图确认；除非用户说效果不好、要求检查，或者页面明显存在技术风险，才需要再截图验证。
- 讲解图的底色优先使用干净的浅暖纸色，接近 `#f5f4ed` / `#faf9f5`，可以有很轻的纸张纹理，但不要用偏黄、偏脏、旧纸感过重的背景。
- 机制图可以保留 Claude 风格的 terracotta 线条、warm ring、手绘感图标，但文字和结构必须优先准确，不要为了风格重绘导致术语或中文内容变形。

## 当前 image generation 状态

已经调用过一次 GPT image 生成 `LLM 的基本机制：next-token prediction` 图。

生成结果默认保存在：

- `/Users/kay/.codex/generated_images/019db7e0-cbcb-7f90-9ccb-67c1bb1106c6/`

该目录下有多个候选 PNG：

- `ig_009fddb3d58e874f0169e9734d7cd4819199fdb91e357c6767.png`
- `ig_02e0678a88aa87e10169eac01a63248191ab6285ebda2b427d.png`
- `ig_0f195a8ff4eb12650169e9d1a949ac8191a28360990e75b693.png`

还有一个较新的生成结果：

- `/Users/kay/.codex/generated_images/019dbcf9-53f8-7bc2-a096-ad04c3f18d9b/ig_037eb77431624d7b0169eabfa0dfd48191b0581930fec3b8e5.png`

这些图片还没有被复制进项目，也还没有嵌入 deck。新窗口接手时应先查看这些图片，选一个复制到：

- `public/generated-images/llm-next-token.png`

然后再改 `slides/01-llm-why-agent.md` 的对应页面。

## 运行与验证

常用命令：

```bash
npm run dev
npm run build
```

最近一次状态：

- `npm run build` 已通过。

每次改完建议至少运行：

```bash
npm run build
```

如果处理视觉问题，建议打开 `npm run dev` 预览，并重点看：

- 是否有空白页
- 是否有文字溢出页面
- 标题是否怪异换行
- 章节页是否过空
- 图片是否真正服务于讲解

但不要把“截图确认”当成默认习惯。这个项目里图片审美和最终取舍由用户现场审核；自动截图主要用于排查布局、溢出、空白页等工程问题。

## 新上下文建议接手顺序

1. 先打开 `README.md` 和 `public/generated-images/image-plan.md`。
2. 检查 `slides/01-llm-why-agent.md` 第一个需要配图的页面。
3. 查看 `/Users/kay/.codex/generated_images/...` 里已经生成的 `next-token prediction` 候选图。
4. 选图并复制到 `public/generated-images/llm-next-token.png`。
5. 把 `LLM 的基本机制：next-token prediction` 页面改成图文结合。
6. 运行 `npm run build`。
7. 继续按 `image-plan.md` 生成并嵌入剩下四张图。

## 不要做的事

- 不要继续使用旧 SVG 讲解图。
- 不要把产品截图重新塞回封面。
- 不要把产品形态章节和 agent 基础定义混在一起。
- 不要泛泛写“agent 很强”，要解释强在哪里、边界在哪里、怎么用。
- 不要把 `agent` 收窄成 `coding agent`。
- 不要写给老师看的“讲什么 / 讲给谁”，页面内容应该面向听众。
- 不要留下孤立的 `---`。
