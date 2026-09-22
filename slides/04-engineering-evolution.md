---
class: section-dark
---

<div class="center-stage"><div class="section-mark">04 · 工程演进</div><h1 class="section-title">从回答到持续执行</h1><p class="lead">任务越来越复杂，设计范围也从提示词扩展到上下文与执行系统。</p></div>

---

# Prompt Engineering：把要求说明白

<p class="lead">单轮任务里，结果直接受任务描述、示例和输出要求影响。</p>

<div class="split-2">
  <div class="frame"><h3>常见任务</h3><ul><li>改写一段邮件</li><li>总结一篇文章</li><li>从文字中提取日期与金额</li></ul></div>
  <div class="frame accent-panel"><h3>提示词组织什么</h3><ul><li>目标、读者与语气</li><li>背景材料和参考示例</li><li>篇幅、字段与输出格式</li></ul></div>
</div>

<p class="note">例子：把这段通知改为 150 字以内，保留时间、地点与报名方式。</p>

<!--
Prompt Engineering（提示工程）关注如何通过指令、背景和示例表达要求。它仍然是后续 Context 和 Harness 设计中的一部分。
-->

---

# Context Engineering：组织当前信息

<p class="lead">任务变成多轮、多步以后，每一步需要的信息也会变化。</p>

<div class="split-2">
  <div class="frame"><h3>信息来自更多地方</h3><ul><li>原始文件与检索结果</li><li>已经确认的结论与任务进展</li><li>工具说明、返回结果和用户偏好</li></ul></div>
  <div class="frame accent-panel"><h3>新的问题</h3><ul><li>关键材料没有进入当前上下文</li><li>无关内容过多，或旧信息与新要求冲突</li><li>任务延续时丢失了条件与出处</li></ul></div>
</div>

<p class="note">上下文工程安排每一步提供什么信息、保留什么记录、何时重新读取资料。</p>

<!--
https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
回扣第三部分：检索、任务摘要、记忆读取和子 Agent 分工，都是组织模型当前信息的不同方式。
-->

---

# 从组织信息到组织执行

<p class="lead">当 Agent 开始修改文件、操作软件和持续运行，设计范围进一步扩展。</p>

<div class="split-3">
  <div class="term-card"><h3>动作能否完成</h3><p>工具、依赖、账号和权限是否可用；失败后怎样处理。</p></div>
  <div class="term-card"><h3>任务能否继续</h3><p>进展与产物存在哪里；中断后如何恢复。</p></div>
  <div class="term-card accent-panel"><h3>结果能否检查</h3><p>怎样回读文件、核对数据，以及引入人工判断。</p></div>
</div>

<p class="note">这些问题涉及模型外的软件设计：Harness Engineering。</p>

<!--
例如批量转换文档：上下文组织解决材料和要求，执行系统还要处理转换程序缺失、单个文件失败、进度保存与结果检查。
-->

---
class: figure-slide
---

# Harness：围绕 Agent 组织执行

<div class="diagram-figure"><img src="/generated-images/harness-system-loop.png" alt="任务约束、工具与权限、状态记录和结果验证围绕 Agent 的执行循环提供支持" /></div>

<!--
Harness Engineering 关注模型之外的任务约束、上下文组织、工具配置、权限、状态、验证与协作。
Agent Runtime 具体驱动调用与执行循环；Harness 描述围绕任务完成而设计的更广泛配套，两者相关但不等同。
https://openai.com/index/harness-engineering/
https://www.anthropic.com/engineering/harness-design-long-running-apps
-->

---
class: figure-slide
---

# Prompt → Context → Harness

<div class="diagram-figure"><img src="/generated-images/prompt-context-harness.png" alt="设计范围从任务指令扩展到当前信息，再扩展到任务执行系统，前面的能力继续保留" /></div>

<!--
这是一条工程关注范围扩展的线索，不是严格按年份划分的替代史。Prompt 仍在 Context 中，Context 仍是 Harness 设计的一部分。
三者分别回答：任务怎样说明；当前提供哪些信息；整套系统怎样执行、延续和检查任务。
-->

---

# AI 工具的能力如何逐步扩展

<table>
  <thead><tr><th>能力形态</th><th>新增的能力</th><th>任务例子</th></tr></thead>
  <tbody>
    <tr><td>Chatbot · 问答</td><td>理解输入并生成内容</td><td>解释概念、改写文字</td></tr>
    <tr><td>Tool Use · 工具调用</td><td>获取外部信息、执行具体操作</td><td>查网页、读文件、计算数据</td></tr>
    <tr><td>Agent · 执行循环</td><td>根据反馈选择后续动作</td><td>查资料、补充缺项、形成简报</td></tr>
    <tr><td>Harness · 系统配套</td><td>组织长任务、权限、恢复与验证</td><td>持续整理资料并检查更新</td></tr>
  </tbody>
</table>

<p class="note">这些能力可以同时存在；产品界面相似，背后的组织方式可能不同。</p>

<!--
保留课程原有演进主线。用能力扩展讲历史逻辑，避免声称所有厂商经历同样阶段或当前问答产品都没有工具。
-->

---

# 不同任务适合不同的处理方式

<div class="split-3">
  <div class="compare-card"><h3>一次问答</h3><p>材料已经齐全，生成一段解释、翻译或摘要即可。</p><div class="example">输出后任务结束</div></div>
  <div class="compare-card"><h3>固定工作流</h3><p>输入和规则稳定，步骤重复，例外情况较少。</p><div class="example">按预设规则执行</div></div>
  <div class="compare-card accent-panel"><h3>Agent</h3><p>任务包含多个步骤，需要根据新信息调整行动。</p><div class="example">执行、观察、继续判断</div></div>
</div>

<p class="note">任务的不确定性、工具需求、成本与等待时间，共同影响处理方式。</p>

<!--
Agent 可以用于学习、研究、文档、数据、编程等不同场景。这里讨论的是任务形态，不是听众的岗位职责。
-->

---

# 课程回顾

<div class="recap-list">
  <div><span>01</span><p><strong>模型参与判断</strong>，软件负责执行工具、处理反馈并继续任务。</p></div>
  <div><span>02</span><p><strong>任务说明、验收方式、工作环境</strong>，共同描述一次协作。</p></div>
  <div><span>03</span><p><strong>上下文决定当前可见信息</strong>，记忆与知识库需要被读取。</p></div>
  <div><span>04</span><p><strong>工具、MCP、Skills 和子 Agent</strong>分别支持操作、连接、复用和分工。</p></div>
  <div><span>05</span><p><strong>工程关注范围持续扩展</strong>，从提示词到信息组织，再到执行系统。</p></div>
</div>

<!--
交流时间约 5 分钟。可从一个听众自己的日常任务开始，讨论需要什么资料、工具与检查方式，不限定用途。
-->

---
class: reading-slide
---

# 课后阅读：原理与工程

<div class="reading-list">
  <a href="https://github.com/bojieli/ai-agent-book"><strong>AI Agent Book · 前四章</strong><span>Agent 入门、上下文、用户记忆和知识库、工具</span></a>
  <a href="https://www.anthropic.com/research/building-effective-agents"><strong>Building effective agents</strong><span>工作流与 Agent 的基本组织方式</span></a>
  <a href="https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents"><strong>Effective context engineering</strong><span>上下文选择、整理与长任务的信息管理</span></a>
  <a href="https://openai.com/index/harness-engineering/"><strong>Harness engineering</strong><span>模型之外的执行系统与验证设计</span></a>
  <a href="https://www.anthropic.com/engineering/harness-design-long-running-apps"><strong>Harness design for long-running apps</strong><span>长任务的进度、状态与反馈</span></a>
</div>

<!--
可选阅读，不占主要讲解时间。书籍采用本地参考版本 f89a8464 的前四章，不按其技术细节逐段展开。
三层框架的背景材料：https://karpathy.bearblog.dev/sequoia-ascent-2026/
https://www.vensas.de/en/blog/karpathy-three-layers
-->

---
class: reading-slide
---

# 课后阅读：工具与使用

<div class="reading-list">
  <a href="https://code.claude.com/docs/en/overview"><strong>Claude Code 文档</strong><span>工具、记忆、MCP 与子 Agent</span></a>
  <a href="https://learn.chatgpt.com/docs/features"><strong>ChatGPT / Codex 桌面功能</strong><span>工作区、任务、文件与工具</span></a>
  <a href="https://modelcontextprotocol.io/docs/learn/architecture"><strong>Model Context Protocol</strong><span>连接架构，以及工具、资料和提示模板</span></a>
  <a href="https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills"><strong>Agent Skills</strong><span>把任务方法、模板和资料组织为可复用能力</span></a>
  <a href="https://docs.packyapi.ai/docs/ccswitch/6-codex-app.html"><strong>本次接入演示说明</strong><span>CC Switch 与 PackyAPI 的客户端配置</span></a>
</div>

<!--
其他资料：https://github.com/farion1231/cc-switch
https://docs.langchain.com/oss/python/langchain/agents
https://docs.langchain.com/oss/python/langchain/long-term-memory
https://docs.langchain.com/oss/python/deepagents/skills
-->
