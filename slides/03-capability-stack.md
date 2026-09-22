---
class: section-dark
---

<div class="center-stage">
  <div>
    <div class="section-mark">03 · 能力扩展</div>
    <div class="divider-line"></div>
    <h1 class="section-title">Agent 的能力扩展</h1>
    <p class="lead">上下文、工具、记忆与知识库，让 Agent 能处理不同类型的工作。</p>
  </div>
</div>

<!--
这一部分解释基本原理，不要求听众配置或开发这些能力。各产品提供的功能不同，不是每个 Agent 都具备下面的全部能力。
参考：《AI Agent Book》第 1—4 章。
-->

---
class: figure-slide
---

# Agent 的能力可以按任务组合

<div class="diagram-figure">
  <img src="/generated-images/agent-capability-stack.png" alt="模型结合上下文、工具、记忆和可选扩展完成任务" />
</div>

<!--
本图是能力地图，不是每个 Agent 都必须逐层安装的结构。模型、上下文和工具构成基本工作方式；MCP、Skills、长期记忆和子 Agent 由产品和任务需要决定。
-->

---

# 上下文：模型这一轮能看到什么

<div class="split-2">
  <div class="frame">
    <h3>任务与约束</h3>
    <p>本次目标、输出格式、范围，以及已经确认的要求。例如把会议记录整理成一页摘要。</p>
    <h3>参考资料</h3>
    <p>本轮读取的文档、图片、表格和检索片段，为回答提供具体依据。</p>
  </div>
  <div class="frame accent-panel">
    <h3>历史与进展</h3>
    <p>之前的沟通、已完成的步骤、当前结论，以及仍待确认的问题。</p>
    <h3>工具信息</h3>
    <p>当前可调用的能力，以及工具刚刚返回的内容、结果或错误。</p>
  </div>
</div>

<p class="note">文件保存在电脑里，只有被读取并传入模型后，才会成为当前上下文。</p>

<!--
参考：《AI Agent Book》第 2 章“上下文：决定 Agent 能力上限的关键”“从 API 视角看上下文的构成”。
https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
这里用工作材料解释上下文，不展开 API 消息角色。上下文还可能包括产品提供的系统规则与持久信息。
-->

---

# 上下文会更新，也有容量限制

<div class="split-3">
  <div class="frame">
    <h3>按需读取</h3>
    <p>先找相关资料，再读取需要的部分。整份文件都传入时，也可能包含大量无关内容。</p>
  </div>
  <div class="frame accent-panel">
    <h3>保留任务摘要</h3>
    <p>长任务可以记录已确认结论、待办事项和来源，让后续步骤继续沿用这些信息。</p>
  </div>
  <div class="frame">
    <h3>必要时回查</h3>
    <p>长对话可能被压缩或截断；摘要会丢失细节，重要数字和条件仍可回到原文核对。</p>
  </div>
</div>

<p class="note">上下文管理关注当前步骤需要哪些信息；更长的聊天记录并不保证更准确。</p>

<!--
参考：《AI Agent Book》第 2 章“上下文压缩策略”。
https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents
例子：整理多次会议记录时，保留决议、负责人、日期和原始记录位置，比让所有讨论反复占据当前上下文更便于继续工作。摘要的准确性仍需要核对。
-->

---

# Tools：连接信息与实际操作

<div class="split-3">
  <div class="frame">
    <h3>感知</h3>
    <p>读取文件、搜索网页、查询数据，让模型获得当前任务需要的信息。</p>
  </div>
  <div class="frame accent-panel">
    <h3>执行</h3>
    <p>生成表格、编辑文档、操作页面，把模型提出的动作变成实际变化。</p>
  </div>
  <div class="frame">
    <h3>协作</h3>
    <p>委托子 Agent 处理独立工作，或在需要补充信息时与人沟通。</p>
  </div>
</div>

<p class="note">模型提出调用 → 软件执行 → 返回结果 → 检查产出。工具报告成功后，仍需确认文件内容或页面状态符合任务目标。</p>

<!--
参考：《AI Agent Book》第 4 章“工具的分类”。
工具是访问或操作的接口，环境是工具运行或访问的地方。终端、浏览器等可以提供工具入口，但不宜与感知、执行、协作混作同一层分类。
本课保留三类主动调用工具，不展开事件触发和异步沟通的技术实现。
-->

---

# MCP：连接外部系统的统一协议

<div class="split-2">
  <div class="frame accent-panel">
    <h3>统一连接方式</h3>
    <p>MCP 的全称是 Model Context Protocol。它约定 AI 应用如何发现和使用外部工具、资料与提示模板。</p>
  </div>
  <div class="frame">
    <h3>复用已有连接</h3>
    <p>文档、日历等系统可以通过 MCP Server（服务端）提供能力；支持协议的 AI 应用可以复用这些连接，减少重复对接。</p>
  </div>
</div>

<p class="note">能接上哪些功能，仍取决于产品支持、服务端提供的能力与账号授权；使用工具也可以采用其他连接方式。</p>

<!--
https://modelcontextprotocol.io/docs/learn/architecture
https://docs.anthropic.com/en/docs/claude-code/mcp
MCP 不代表连接后自动获得外部系统全部能力，也不保证不同客户端支持完全一致。
-->

---
class: figure-slide
---

# MCP 提供工具、资料与提示模板

<div class="diagram-figure">
  <img src="/generated-images/mcp-primitives.png" alt="MCP 三类能力：Tools 可调用动作、Resources 可读取资料、Prompts 可复用提示模板" />
</div>

<!--
Tools：可调用动作，如搜索文档、创建日程。
Resources：可读取资料，如一份手册、一个数据文件。
Prompts：供用户选用的提示模板，如会议摘要模板。
一个 MCP Server 可以只提供其中部分能力；各客户端的展示方式不同。
https://modelcontextprotocol.io/docs/learn/server-concepts
-->

---

# MCP 连接中的三个角色

<div class="split-3">
  <div class="frame accent-panel">
    <h3>AI 应用 / Client</h3>
    <p>接收任务，通过客户端与服务端交互。例如请求查询下周的空闲会议时间。</p>
  </div>
  <div class="frame">
    <h3>MCP Server</h3>
    <p>提供日历查询等能力，接收调用请求，并与实际的日历系统连接。</p>
  </div>
  <div class="frame">
    <h3>外部系统</h3>
    <p>保存日程、文档或业务数据，按实际账号权限处理查询和修改。</p>
  </div>
</div>

<p class="note">结果沿连接返回 AI 应用，再进入模型的上下文。模型可以据此继续操作，或向用户说明查询结果。</p>

<!--
https://modelcontextprotocol.io/docs/learn/architecture
为非技术听众将 Host 与其内部 Client 放在同一卡片。AI 应用承载模型和连接管理；MCP Client 负责与 Server 通信，Server 再访问外部能力。
-->

---

# 例子：连接一个文档系统

<div class="split-2">
  <div class="frame accent-panel">
    <h3>可提供的能力</h3>
    <ul>
      <li><strong>Resources</strong>：一份可读取的报销制度。</li>
      <li><strong>Tools</strong>：搜索文档、读取内容、创建摘要文件。</li>
      <li><strong>Prompts</strong>：预设的制度摘要模板。</li>
    </ul>
  </div>
  <div class="frame">
    <h3>一次实际任务</h3>
    <p>用户询问报销需要哪些材料。Agent 搜索相关制度、读取条款，整理材料清单，并标明原文位置。</p>
  </div>
</div>

<p class="note">这是一个示意连接；实际提供哪几类能力，由具体服务决定。文档访问范围仍受账号权限约束。</p>

<!--
本页为通用办公示例，不声称某个具体文档产品必然提供全部三类能力。
https://modelcontextprotocol.io/docs/learn/server-concepts
-->

---

# MCP 适用的连接场景

<div class="split-3">
  <div class="frame">
    <h3>持续使用同一系统</h3>
    <p>工作经常涉及文档、日历或内部数据，稳定的连接可以减少反复导入材料。</p>
  </div>
  <div class="frame accent-panel">
    <h3>多种应用共享能力</h3>
    <p>多个支持 MCP 的 AI 应用，可以连接同一个服务端，复用已有的接入工作。</p>
  </div>
  <div class="frame">
    <h3>已有合适的服务端</h3>
    <p>外部系统已经提供所需能力，客户端也支持对应的连接和授权方式。</p>
  </div>
</div>

<p class="note">一次性的文件分析可以直接上传或读取文件；是否使用 MCP，取决于实际的连接需求。</p>

<!--
https://modelcontextprotocol.io/docs/learn/architecture
保持在使用层面，不展开部署、协议版本或具体认证配置。
-->

---
class: figure-slide
---

# Skill：可复用的任务资料包

<div class="diagram-figure">
  <img src="/generated-images/skill-pack.png" alt="Skill 可以包含任务说明、工作步骤、模板、参考资料和可选脚本" />
</div>

<!--
https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills
Skill 通常以说明文件为入口，按任务需要读取相关材料。具体目录要求和加载方式取决于产品；本课不展开文件格式。
-->

---

# Skill 如何参与一次任务

<div class="split-3">
  <div class="frame">
    <h3>识别适用任务</h3>
    <p>系统根据任务与 Skill 描述，判断是否需要读取相关做法，例如整理会议纪要。</p>
  </div>
  <div class="frame accent-panel">
    <h3>读取工作方法</h3>
    <p>将步骤说明、示例、模板和必要资料放入上下文，作为这次执行的参考。</p>
  </div>
  <div class="frame">
    <h3>调用工具并检查</h3>
    <p>Agent 使用已有工具生成文档，再核对任务要求、关键事实和输出格式。</p>
  </div>
</div>

<p class="note">Skill 可以让做法复用；结果仍取决于资料、模型、工具和检查过程。</p>

<!--
https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills
参考：《AI Agent Book》第 2 章“动态提示词与 Agent Skills”。
加载和触发方式由产品实现决定，也可以由用户主动指定。Skill 不会自动赋予额外权限，也不保证执行结果正确。
-->

---

# Prompt、Tool、Skill、Memory 的区别

<table>
  <thead>
    <tr><th>概念</th><th>主要作用</th><th>办公例子</th></tr>
  </thead>
  <tbody>
    <tr><td>Prompt · 提示词</td><td>说明当前任务和要求</td><td>把这份会议记录整理成一页摘要。</td></tr>
    <tr><td>Tool · 工具</td><td>执行具体的读取或操作</td><td>打开记录文件，创建整理后的文档。</td></tr>
    <tr><td>Skill · 技能</td><td>复用一类任务的工作方法</td><td>按固定结构提取议题、决议和待办。</td></tr>
    <tr><td>Memory · 记忆</td><td>保留并取回跨任务信息</td><td>沿用用户偏好的“结论先行”格式。</td></tr>
  </tbody>
</table>

<p class="note">这些能力可以组合使用；同一个任务不一定需要全部用到。</p>

<!--
参考：《AI Agent Book》第 2—4 章。
这里按主要作用区分，实际产品的边界可能有所重叠。例如 Skill 中也包含提示文本，但其用途是复用任务方法及相关材料。
-->

---

# 例子：会议纪要 Skill

<div class="split-2">
  <div class="frame">
    <h3>资料包中的内容</h3>
    <ul>
      <li>步骤：提取议题、决议和待办，区分已确认与待确认事项。</li>
      <li>模板：使用固定栏目；示例：展示一份完整的纪要。</li>
    </ul>
  </div>
  <div class="frame accent-panel">
    <h3>每次任务中的变化</h3>
    <ul>
      <li>读取这次会议的原始记录，填入实际内容。</li>
      <li>核对负责人和日期；原文缺失的信息保留为空或标明待确认。</li>
    </ul>
  </div>
</div>

<p class="note">复用的是整理方法和格式；每次会议的事实仍来自本次记录。</p>

<!--
这是教学示例，不依赖特定产品内置的 Skill。
https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills
讲解时可提到：资料包可以包含脚本，但并非所有 Skill 都需要脚本。
-->

---

# 临时要求与可复用的方法

<div class="split-2">
  <div class="frame">
    <h3>一次性的要求</h3>
    <p>偶尔改写一段邮件、总结一篇文章，任务说明和相关材料通常就能表达清楚。</p>
    <p>内容和格式随这一次任务变化，直接在对话中补充即可。</p>
  </div>
  <div class="frame accent-panel">
    <h3>反复使用的方法</h3>
    <p>每周整理纪要、每月制作固定格式的汇报，可以把步骤、示例和模板整理为 Skill。</p>
    <p>流程变化时，更新共享的方法和资料，后续任务再读取新版本。</p>
  </div>
</div>

<p class="note">任务频率、方法是否稳定、是否依赖固定资料，决定了复用的价值。</p>

<!--
参考：《AI Agent Book》第 2 章“动态提示词与 Agent Skills”。
避免把 Skill 描述成必然优于普通提示词的升级路径。简单或临时任务不必增加资料包维护工作。
-->

---

# 当前上下文、用户记忆与知识库

<div class="split-3">
  <div class="frame">
    <h3>当前上下文</h3>
    <p>模型这一轮正在使用的信息，例如本次聊天、读到的材料与任务进展。</p>
  </div>
  <div class="frame accent-panel">
    <h3>用户记忆</h3>
    <p>跨任务保存的偏好与背景，例如喜欢简短回复、汇报采用结论先行的格式。</p>
  </div>
  <div class="frame">
    <h3>共享知识库</h3>
    <p>可供多人查询的资料，例如公司制度、操作手册与常见问题说明。</p>
  </div>
</div>

<p class="note">记忆和知识库中的内容，需要被取回并传入模型，才进入当前上下文；保存资料不会自动改变模型参数。</p>

<!--
参考：《AI Agent Book》第 3 章“用户记忆系统”“RAG 基础”。
用户记忆不一定完全私有或自动生成，具体取决于产品。这里强调信息用途与使用时机，不把短期状态和工作记忆画成互不重叠的存储层。
-->

---

# 记忆的保存、读取与更新

<div class="split-3">
  <div class="frame">
    <h3>保存可复用信息</h3>
    <p>“以后汇报都用一页摘要”可以成为长期偏好；“这周五前完成”属于本次任务安排。</p>
  </div>
  <div class="frame accent-panel">
    <h3>任务需要时读取</h3>
    <p>下次整理汇报时，取回输出偏好并加入上下文。保存过的信息也可能尚未被取回。</p>
  </div>
  <div class="frame">
    <h3>信息变化时更新</h3>
    <p>联系人或习惯改变后，旧记录需要修订；一次临时例外不一定适合作为长期规则。</p>
  </div>
</div>

<p class="note">跨会话记忆是否可用、如何保存和删除，取决于具体产品及其设置。</p>

<!--
参考：《AI Agent Book》第 3 章“记忆的层次结构”“知识应该如何更新”。
https://docs.anthropic.com/en/docs/claude-code/memory
讲解可补充：记忆可能由用户指定保存，也可能由产品自动提取，不应假定任何一轮聊天都会永久保留。
-->

---

# RAG：查到资料后再回答

<div class="flow-row">
  <div class="flow-step"><strong>提出问题</strong><p>出差报销需要哪些材料？</p></div>
  <div class="flow-step"><strong>检索资料</strong><p>查找相关制度和操作说明。</p></div>
  <div class="flow-step"><strong>加入上下文</strong><p>取回相关条款、版本和来源。</p></div>
  <div class="flow-step"><strong>形成回答</strong><p>整理材料清单，并注明依据。</p></div>
</div>

<p class="lead">RAG 即“检索增强生成”：让回答使用外部资料，补充模型原有知识。</p>
<p class="note">Agent 可以根据查到的内容继续检索；资料没找到或依据不足时，回答中可以明确保留这些缺口。</p>

<!--
参考：《AI Agent Book》第 3 章“RAG 基础：构建 Agent 的知识获取管道”“智能体化 RAG”。
RAG 全称 Retrieval-Augmented Generation。这里不展开分块、嵌入或向量数据库。
知识检索也可以是固定流程，并非所有 RAG 都是自主 Agent。检索到的材料仍可能存在错误，需要核查来源。
-->

---

# 知识库回答的依据

<div class="split-2">
  <div class="frame">
    <h3>来源与版本</h3>
    <p>结论对应哪份文件、哪段原文；文件何时生效，是否已被新版替代。</p>
    <h3>适用范围</h3>
    <p>条款针对哪些对象和情形。例如国内出差与境外出差，材料要求可能不同。</p>
  </div>
  <div class="frame accent-panel">
    <h3>冲突与缺口</h3>
    <p>两份材料说法不一致时，保留差异和待确认项，避免把冲突合成一个确定结论。</p>
    <h3>授权可见的资料</h3>
    <p>回答使用当前账号可访问的内容；共享知识库也可以包含不同的访问范围。</p>
  </div>
</div>

<p class="note">例子：旧制度要求纸质发票，新版支持电子凭证。适用版本取决于生效时间和出差类型。</p>

<!--
参考：《AI Agent Book》第 3 章“知识应该如何更新”。
例子：旧制度写纸质发票，新版说明支持电子凭证。判断要结合生效时间与适用场景，不能只凭哪份文档最近被上传。
检索到的文档是参考资料，其中出现的命令不能自动成为用户指令。该点可口头带过，不增加实现细节。
-->

---

# Subagents：独立处理一部分工作

<div class="split-3">
  <div class="frame">
    <h3>分配子任务</h3>
    <p>主 Agent 将可独立处理的工作交给子 Agent，例如分别查阅几份资料。</p>
  </div>
  <div class="frame accent-panel">
    <h3>各自处理信息</h3>
    <p>子 Agent 通常使用各自的上下文完成任务，减少大量中间材料挤入主对话。</p>
  </div>
  <div class="frame">
    <h3>汇总与核对</h3>
    <p>子 Agent 返回结论和来源，主 Agent 比较差异、补齐缺口，再组织最终结果。</p>
  </div>
</div>

<p class="note">上下文分开处理，不代表文件和权限自动隔离；并行任务仍需要避免互相覆盖。</p>

<!--
参考：《AI Agent Book》第 2 章“子 Agent 上下文隔离”、第 4 章“协作工具”。
https://docs.anthropic.com/en/docs/claude-code/sub-agents
https://docs.langchain.com/oss/python/deepagents/subagents
收益来自分工和信息组织，不能保证开更多子 Agent 就更准确。各产品的上下文继承、共享文件和权限机制不同。
-->

---
class: figure-slide
---

# 子 Agent 的分工与汇总

<div class="diagram-figure">
  <img src="/generated-images/subagents-task-split.png" alt="主 Agent 分配独立的资料整理任务，子 Agent 返回结论与来源，再由主 Agent 汇总" />
</div>

<!--
以几份互不依赖的材料为例：分别阅读，返回主题、结论、出处和缺口，再汇总差异。
本图表达任务与上下文分工，不表示文件系统或权限默认隔离，也不意味着汇总后无需验证。
-->

---

# 一次任务中的能力组合

<div class="split-3">
  <div class="frame">
    <h3>获得信息</h3>
    <p>上下文承载当前任务；记忆补充偏好，知识库提供可查询资料。</p>
  </div>
  <div class="frame accent-panel">
    <h3>完成操作</h3>
    <p>模型判断下一步，工具读取和修改内容；MCP 可以承担外部系统的连接。</p>
  </div>
  <div class="frame">
    <h3>复用与分工</h3>
    <p>Skill 提供已有方法；需要独立处理多项工作时，可以使用子 Agent。</p>
  </div>
</div>

<p class="note">整理一份文档可能只需模型、上下文和文件工具。更复杂的任务，再按实际需要组合其他能力。</p>

<!--
参考：《AI Agent Book》第 1—4 章。
各能力不是所有 Agent 都必需的固定层。比如本地读取文件无需经过 MCP，一次短任务也未必需要长期记忆或子 Agent。
-->

---

# 不同能力解决不同问题

<div class="split-2">
  <div class="frame">
    <h3>访问和操作</h3>
    <p>Tools 提供具体动作；需要连接外部系统时，MCP 可以统一接入方式。</p>
    <h3>依据和连续性</h3>
    <p>知识库提供业务资料；Memory 保存与取回跨任务有用的信息。</p>
  </div>
  <div class="frame accent-panel">
    <h3>稳定重复的方法</h3>
    <p>Skills 复用步骤、模板与资料，减少同类任务反复说明的工作。</p>
    <h3>可独立处理的工作</h3>
    <p>Subagents 提供分工方式；汇总时仍需要核对来源、差异与最终结果。</p>
  </div>
</div>

<p class="note">这些能力没有统一的添加顺序，选择取决于任务缺少什么、产品已经提供什么。</p>

<!--
本页替代原来的固定能力优先级，避免形成所有 Agent 都必须逐层补齐的误解。
参考：《AI Agent Book》第 1—4 章。
-->
