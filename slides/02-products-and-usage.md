---
class: section-dark
---

<div class="center-stage">
  <div>
    <div class="section-mark">02 · 产品与用法</div>
    <div class="divider-line"></div>
    <h1 class="section-title">Agent 产品与基本使用</h1>
    <p class="lead tight">不同的入口，相似的工作循环。<br>从产品界面到任务说明、验收方式和工作环境。</p>
  </div>
</div>

<!--
本章约 15 分钟，演示时间另计。
从产品形态切入，说明 Agent 可以通过终端、桌面应用、编辑器、聊天入口或流程画布使用。
Claude Code 与 Codex 作为具体例子，讲解文件、工具、任务与结果之间的关系。
-->

---

# Agent 可以出现在不同的入口里

<table>
  <thead>
    <tr><th>产品</th><th>常见入口</th><th>交互方式</th></tr>
  </thead>
  <tbody>
    <tr><td>Claude Code</td><td>终端、编辑器、桌面与网页</td><td>围绕文件和工具持续执行任务</td></tr>
    <tr><td>Codex</td><td>桌面、终端、编辑器与网页</td><td>组织任务，查看过程与产出</td></tr>
    <tr><td>Cursor</td><td>代码编辑器</td><td>在编辑文件的同时与 Agent 协作</td></tr>
    <tr><td>OpenClaw</td><td>聊天应用、网页控制台</td><td>通过消息连接个人助手与工具</td></tr>
    <tr><td>n8n</td><td>流程画布</td><td>把 Agent 和固定步骤接成流程</td></tr>
  </tbody>
</table>

<p class="note">入口决定交互方式；模型、工具和权限共同影响实际能力。</p>

<!--
这里展示常见入口，不是完整功能清单。同一产品可能支持多种入口，能力也会随版本和配置变化。
n8n 是工作流平台，流程中可以包含 Agent 节点，并非每条工作流都由 Agent 决策。
产品资料：
https://code.claude.com/docs/en/overview
https://learn.chatgpt.com/docs/features
https://cursor.com/docs
https://docs.openclaw.ai/
https://docs.n8n.io/advanced-ai/
-->

---
class: figure-slide
---

# 不同产品中常见的工作机制

<div class="diagram-figure">
  <img src="/generated-images/agent-product-core.png" alt="不同产品都可以组织模型、上下文、工具和反馈循环，具体实现各有差异" />
</div>

<!--
相似的是机制：模型根据上下文选择行动，工具执行后返回结果，系统再继续下一步。
各产品的模型、调度方式、执行环境和权限系统并不相同，也不意味着共享同一份软件内核。
可用读文件、提取信息、写摘要这三步解释图中的循环。
-->

---

# Claude Code：围绕文件与工具工作

<div class="split-2">
  <div class="image-frame">
    <img src="/products/claude-code.webp" alt="Claude Code 终端界面：任务对话与执行过程" />
  </div>
  <div class="frame">
    <h3>从任务描述到文件产出</h3>
    <ul class="wide-list">
      <li>读取目录与文件，查找相关内容。</li>
      <li>编辑文件，运行命令处理数据。</li>
      <li>通过工具连接外部资料与服务。</li>
      <li>结合任务规则，检查并汇报结果。</li>
    </ul>
  </div>
</div>

<!--
Claude Code 的主要定位是编程助手，也能利用文件和命令工具完成通用任务，例如汇总一组文本、转换数据格式或批量整理文件。
桌面、终端、编辑器和网页是不同入口，具体工具与文件可访问范围取决于入口和配置。
这里的“读取目录与文件”不是一次把全部文件自动读入模型上下文。
资料：https://code.claude.com/docs/en/overview
工具：https://code.claude.com/docs/en/tools-reference
-->

---

# Claude Code：任务结果与执行条件

<div class="split-2">
  <div class="frame accent-panel">
    <h3>可交给它的工作</h3>
    <ul class="wide-list">
      <li>提取多份文档的标题与摘要。</li>
      <li>按约定规则整理一批文件。</li>
      <li>编写并运行脚本，合并表格。</li>
    </ul>
  </div>
  <div class="frame">
    <h3>影响结果的条件</h3>
    <ul class="wide-list">
      <li>原始文件是否可访问、可解析。</li>
      <li>处理规则与输出格式是否明确。</li>
      <li>工具是否具备所需权限与依赖。</li>
    </ul>
  </div>
</div>

<p class="note">命令运行成功，只说明执行完成；文件内容和处理结果仍有各自的检查方式。</p>

<!--
例如“按月份整理发票”还涉及月份按开票日期还是报销日期计算。规则不明确时，可以先查看样例，再补充定义。
合并表格可检查输入输出行数、重复记录、日期格式和金额合计；文档摘要则需要对照原文确认事实。
这些限制适用于多种 Agent 产品，并非 Claude Code 独有。
-->

---

# Codex：组织任务与查看产出

<div class="split-2">
  <div class="image-frame">
    <img src="/products/codex.webp" alt="Codex 桌面界面：任务列表、对话与工作区" />
  </div>
  <div class="frame">
    <h3>在工作区里推进任务</h3>
    <ul class="wide-list">
      <li>读取资料，修改文件，运行工具。</li>
      <li>在不同任务中跟踪进展与结果。</li>
      <li>通过技能与插件扩展处理方式。</li>
      <li>按计划继续任务或执行周期工作。</li>
    </ul>
  </div>
</div>

<!--
现场演示可选一组本地材料：列出文件、整理要点、生成一份文档，再打开产出检查。
桌面应用提供任务与项目组织能力；编程任务可以查看文件差异，通用文档任务可以直接打开产出。
定时任务需要可用的运行环境。本地任务需要电脑和应用保持运行，且资料与工具仍然可访问。
不同入口、账号和版本的能力不完全一致，本页不逐项比较功能覆盖。
资料：https://learn.chatgpt.com/docs/features
定时任务：https://learn.chatgpt.com/docs/automations?surface=app
-->

---

# Codex：多任务怎样衔接

<div class="split-2">
  <div class="frame accent-panel">
    <h3>可以分别推进</h3>
    <ul class="wide-list">
      <li>一项任务查资料，另一项整理表格。</li>
      <li>每项任务保留自己的进展与产出。</li>
      <li>周期任务按约定时间继续执行。</li>
    </ul>
  </div>
  <div class="frame">
    <h3>衔接时需要的信息</h3>
    <ul class="wide-list">
      <li>汇总任务所需的文件与结论。</li>
      <li>共同使用的字段定义和统计口径。</li>
      <li>文件修改范围与最终检查方式。</li>
    </ul>
  </div>
</div>

<p class="note">任务分开后，上下文需要传递；同时处理文件时，也需要协调修改范围。</p>

<!--
多个任务和多个子 Agent 是两种组织方式，均不意味着数据天然共享或文件天然隔离。
桌面工作区可以组织并行工作。Git worktree 是一种隔离代码修改的办法，普通文件夹中的并行任务仍可能修改同一文件。
例如任务 A 搜集公开资料、任务 B 处理本地表格，汇总时需要提供双方产物，以及单位、时间范围和来源。
资料：https://learn.chatgpt.com/docs/environments/git-worktrees
-->

---
class: figure-slide
---

# Codex：从任务到可检查的结果

<div class="diagram-figure">
  <img src="/generated-images/codex-task-to-result.png" alt="明确任务，读取资料，调用工具，检查产出，再根据反馈继续" />
</div>

<!--
这是一种常见工作流程。读取资料、执行和检查可能往返多次，任务也可以在中途补充信息或调整方向。
按计划执行不代表结果必然正确。可检查的结果既可以是测试通过的代码，也可以是附来源的简报或能够回算的表格。
演示时展示任务说明、一次工具调用、实际产出和检查过程，约 15 分钟。
-->

---

# AI 协作的三个部分

<div class="split-3">
  <div class="frame">
    <div class="eyebrow">Spec</div>
    <h3>任务说明</h3>
    <p>目标是什么，交付什么，哪些范围和限制需要遵守。</p>
    <p class="note">主题、材料范围、输出格式。</p>
  </div>
  <div class="frame accent-panel">
    <div class="eyebrow">Verifier</div>
    <h3>验收方式</h3>
    <p>通过什么证据和检查方法，判断结果是否符合要求。</p>
    <p class="note">来源回查、数字核对、人工审阅。</p>
  </div>
  <div class="frame">
    <div class="eyebrow">Environment</div>
    <h3>工作环境</h3>
    <p>任务执行时可用的资料、工具、记忆、工作区和权限。</p>
    <p class="note">原始文件、搜索工具、输出目录。</p>
  </div>
</div>

<!--
这三个部分共同描述一次 AI 协作：任务说明定义预期，验收方式提供反馈，工作环境提供行动条件。
Verifier 可以是确定性检查，例如计算合计、核对文件数；也可以是人工审阅，例如判断摘要是否准确、表达是否适合读者。
对于没有唯一答案的任务，可以明确评价维度，例如信息完整性、事实依据、表达风格，而不必强行设置自动测试。
本页采用 vensas 对 Karpathy 实践的三部分归纳，结合其公开访谈整理；这不是 Karpathy 原文正式命名的三层模型。
背景阅读：
https://karpathy.bearblog.dev/sequoia-ascent-2026/
https://www.vensas.de/en/blog/karpathy-three-layers
-->

---

# 例子：把一组资料整理成简报

<div class="split-2">
  <div class="frame accent-panel">
    <h3>任务说明</h3>
    <p>根据资料目录中的文档，整理一页“远程办公实践”简报，包含三个主要发现和待确认事项。</p>
    <p>关键事实附来源；资料没有涉及的内容标为未知。结果保存到输出目录。</p>
  </div>
  <div class="frame">
    <h3>验收方式</h3>
    <p>结论能回查原文；数字与日期一致；人工检查是否遗漏关键信息。</p>
    <h3>工作环境</h3>
    <p>原始文档、搜索与文档工具、简报模板，以及可写入的输出目录。</p>
  </div>
</div>

<!--
这个例子用于解释三层框架，不是全课的唯一任务。文件整理、数据统计、个人学习也可以用同样三个部分描述。
开始时可以先列出资料并查看样例，以发现缺失材料、扫描件无法解析或文档之间的冲突。
任务目标较大时，可拆成资料清点、信息提取、生成简报、核对产出。拆分依据是可检查的中间结果。
搜索工具可用于资料目录内查找。本例以目录中的文档为事实范围；如果需要联网补充，应在任务说明中增加范围，并区分原始资料和外部来源。
验收时抽查来源不足以保证所有内容正确；本例优先核对简报中所有关键事实，主观判断由阅读者结合用途审阅。
-->

---

# 产品差异体现在工作方式中

<table>
  <thead>
    <tr><th>产品</th><th>常见使用方式</th><th>查看结果的位置</th></tr>
  </thead>
  <tbody>
    <tr><td>Claude Code</td><td>围绕文件、命令和项目持续协作</td><td>对话记录、执行输出、文件修改</td></tr>
    <tr><td>Codex</td><td>在工作区中组织多个任务与产出</td><td>任务列表、文件预览、修改对照</td></tr>
    <tr><td>Cursor</td><td>在编辑器中边阅读、边修改、边讨论</td><td>编辑器、终端、文件修改对照</td></tr>
  </tbody>
</table>

<p class="lead">同一项任务可能有多个入口。实际使用取决于资料放在哪里、需要哪些工具，以及怎样检查结果。</p>

<!--
本页比较的是典型使用方式，不代表功能互斥，也不作能力排名。Claude Code 同样有桌面入口，Codex 同样提供命令行与编辑器入口。
对于通用办公，先确认产品能否读取所需文件、调用相应工具并生成可用格式；界面形式本身并不保证任务效果。
资料：https://code.claude.com/docs/en/overview
https://learn.chatgpt.com/docs/features
https://cursor.com/docs
-->
