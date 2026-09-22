---
class: section-dark
---

<div class="center-stage"><div class="section-mark">01 · 基本机制</div><h1 class="section-title">从 LLM 到 Agent</h1><p class="lead">生成机制、工具调用与执行循环，共同解释 Agent 如何工作。</p></div>

---
class: figure-slide
---

# 大语言模型（LLM）如何生成内容

<div class="diagram-figure"><img src="/generated-images/llm-next-token.png" alt="模型根据当前上下文预测下一个 token，并将新 token 加入序列继续生成" /></div>

<!--
LLM 是大语言模型。Token 是模型处理内容的片段，可能是字、词的一部分或标点，不等于完整词语。
模型依据上下文计算下一个 token 的概率，选择后继续生成；这描述生成机制，不代表模型只会做简单接龙。
-->

---

# 生成机制能支持哪些能力

<div class="split-2">
  <div class="frame accent-panel"><h3>语言与信息处理</h3><ul><li>理解上下文，提取关键信息</li><li>归纳、改写、翻译与推理</li><li>生成文字、结构化数据和代码</li></ul></div>
  <div class="frame"><h3>任务执行所需的配套</h3><ul><li>工具提供文件与外部系统的操作入口</li><li>状态记录保存进展与中间结果</li><li>检查过程提供纠正错误的依据</li></ul></div>
</div>

<p class="note">模型生成一个操作请求后，还需要软件真正执行这个请求。</p>

<!--
例如模型能写整理文件的脚本；脚本是否执行、访问哪个目录、结果如何回传，由模型外的软件决定。
-->

---

# 纯文本问答的边界

<div class="split-2 media-split">
  <div class="image-frame"><img src="/products/chatgpt.png" alt="聊天产品的对话界面示例" /></div>
  <div><p class="lead">在没有接入工具的问答模式中：</p><ul><li>材料主要来自当前对话</li><li>输出通常是一段文字或方案</li><li>外部操作由人继续完成</li><li>系统难以观察操作后的实际结果</li></ul></div>
</div>

<p class="note">界面长得像聊天框，并不能说明它有没有执行能力。</p>

<!--
截图仅说明对话入口。这里描述纯文本问答模式，不声称当前 ChatGPT 产品只能问答。
-->

---
class: figure-slide
---

# 从生成回答到执行任务

<div class="diagram-figure"><img src="/generated-images/from-chat-to-agent.png" alt="纯文本问答输出回答；Agent 通过工具操作环境并根据返回结果继续推进" /></div>

<!--
例如整理文件：模型选择读取目录，软件调用文件工具并返回清单；模型根据清单继续分类或询问缺失条件。
-->

---

# Agent 是什么

<p class="lead">Agent 是由模型参与选择下一步动作、使用工具并处理反馈的 AI 软件系统。</p>

<div class="split-3">
  <div class="term-card"><h3>模型</h3><p>结合当前信息，生成回答或提出下一步操作。</p></div>
  <div class="term-card"><h3>上下文</h3><p>本轮可见的任务、资料、历史进展和工具结果。</p></div>
  <div class="term-card accent-panel"><h3>工具与运行层</h3><p>执行操作、记录进展，并驱动下一轮判断。</p></div>
</div>

<p class="note">软件由程序、数据和规则组成；界面是与用户交互的部分。</p>

<!--
这里的 Agent 指基于 LLM 的软件系统。程序运行起来会接收输入、调用工具并产生输出；持续推进还需要结束条件、错误处理和相应的权限控制。
-->

---

# 谁决定任务的下一步

<div class="split-3">
  <div class="compare-card"><div class="eyebrow">问答</div><h3>人继续发起</h3><p>收到回答后，由人决定下一问或下一项操作。</p><div class="example">例如：解释一段文字</div></div>
  <div class="compare-card"><div class="eyebrow">工作流</div><h3>预设规则控制</h3><p>程序按提前设计的步骤、条件和分支运行。</p><div class="example">例如：每天汇总固定报表</div></div>
  <div class="compare-card accent-panel"><div class="eyebrow">Agent</div><h3>模型参与选择</h3><p>根据当前情况和工具反馈，动态选择下一步。</p><div class="example">例如：查资料并整理比较结果</div></div>
</div>

<p class="note">工作流可以包含 Agent 节点；Agent 也可以调用固定流程。</p>

---
class: figure-slide
---

# 模型在 Agent 系统中的位置

<div class="diagram-figure"><img src="/generated-images/llm-inside-agent-system.png" alt="Agent 系统中，模型与任务调度、工具、状态、权限和执行环境协同工作" /></div>

<!--
Agent Runtime 是驱动模型、工具与反馈循环的运行层。执行环境是工具实际运行和访问资源的地方，例如本机、浏览器或沙箱。两者不能混作同一个概念。
-->

---
class: figure-slide
---

# Agent Loop：判断、行动与反馈

<div class="diagram-figure"><img src="/generated-images/agent-loop.png" alt="Agent 根据任务判断下一步，调用工具，观察返回结果，再继续判断或结束" /></div>

<!--
ReAct 是一种常见的 Agent Loop，将推理与行动交替组织。Agent Loop 是更广的概念，两者不完全等同。
工具结果重新加入上下文；模型可以继续操作、请求补充信息或结束。实际系统还设置次数、时间或成本限制。
“思考”是对模型选择动作的简化描述，不意味着应用必须显示模型的内部推理。
-->

---
class: figure-slide
---

# Human-in-the-loop：人工参与执行

<div class="diagram-figure"><img src="/generated-images/human-in-the-loop.png" alt="需要确认的操作在执行前交由人批准、修改或拒绝，再继续任务循环" /></div>

<!--
可以为对外发送、支付、权限变更等操作设置人工确认。审核点由应用和任务配置决定，并非每次读文件或每个普通操作都需要审批。
人也可以参与澄清目标、选择方案和结果验收；图中展示执行前确认的一种形式。
-->

---

# 多步任务如何持续推进

<div class="grid-2">
  <div class="term-card"><h3>Agent Runtime · 运行层</h3><p>安排模型调用和工具执行，处理返回结果、错误与结束条件。</p></div>
  <div class="term-card"><h3>Tools · 工具</h3><p>提供读取文件、查询网页、处理数据等实际操作。</p></div>
  <div class="term-card"><h3>State · 任务状态</h3><p>保存计划、已完成步骤、待处理问题和中间产物。</p></div>
  <div class="term-card accent-panel"><h3>Feedback · 反馈</h3><p>用页面状态、文件内容、计算结果或报错调整下一步。</p></div>
</div>

<!--
例如生成表格后再次读取它，检查行数、字段和合计。状态支撑当前任务；跨任务保留信息的 Memory 在第三部分展开。
-->

---

# Shell：系统命令的执行入口

<div class="split-2 media-split">
  <div><p class="lead">Shell 接收命令，启动程序，并返回执行结果。</p><ul><li>批量整理文件与目录</li><li>运行脚本、转换格式、计算数据</li><li>调用已安装的软件和命令行工具</li></ul><p class="note">界面负责交互，Agent 组织步骤，Shell 执行具体命令。</p></div>
  <div class="image-frame"><img src="/products/openclaw-web.avif" alt="通过图形界面与 Agent 交互的产品示例" /></div>
</div>

<!--
Shell 可以调用操作系统已有的文件、进程和网络能力。进程是正在运行的程序；命令行是用文本输入操作的方式。
API 是软件之间约定的调用接口。Agent 也能通过浏览器、文件接口和外部 API 执行任务，不必一律经过 Shell。
截图用于说明界面与执行能力可以分离，不能根据界面形态推断具体配置。
-->

---
class: figure-slide
---

# 工具与环境共同决定可执行的范围

<div class="diagram-figure"><img src="/generated-images/shell-access-boundary.png" alt="Shell、浏览器、文件接口和外部 API 都可提供执行能力，权限与环境限定其访问范围" /></div>

<!--
环境包括文件、网络、账号状态和可用程序。相同模型在不同环境下能完成的任务可能不同；能生成命令与有权限执行命令也是不同的事情。
-->
