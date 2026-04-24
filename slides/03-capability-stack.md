---
class: section-dark
---

<div class="center-stage">
  <div>
    <div class="section-mark">Part 3</div>
    <div class="divider-line"></div>
    <h1 class="section-title">Agent 的能力扩展层</h1>
    <p class="lead tight">这里不是“一堆插件介绍”，而是系统能力是怎么一层层加出来的。</p>
  </div>
</div>

---
class: diagram-slide
---

<div class="image-frame full-diagram">
  <img src="/generated-images/agent-capability-stack.png" alt="Agent capability stack：能力不是一堆插件" />
</div>

---
class: page-tight
---

# Tools：让 Agent 真正做事

<div class="tools-three">
  <div class="term-card">
    <h3>信息类工具</h3>
    <p>读文件、搜网页、查数据库、调用 API。</p>
  </div>
  <div class="term-card">
    <h3>执行类工具</h3>
    <p>跑脚本、发请求、点网页、执行命令。</p>
  </div>
  <div class="term-card">
    <h3>环境类工具</h3>
    <p>终端、浏览器、IDE、沙箱、远程环境。</p>
  </div>
</div>

<div class="callout centered-note">
  <p><strong>教学重点：</strong>没有工具，Agent 往往只能说；有了工具，它才能做。</p>
</div>

<div class="source-line">
  资料：Anthropic Claude Code 官方总览；LangChain Agents / Tools 官方文档。
</div>

---

# MCP 是什么

<div class="split-2">
  <div class="frame accent-panel">
    <div class="eyebrow">标准定义</div>
    <p>
      <code>MCP</code> 是 <code>Model Context Protocol</code>，一种把外部工具、资源和提示词标准化接给模型或 agent 的协议。
    </p>
    <div class="takeaway">
      它更像“统一插座标准”，不是某个具体功能。
    </div>
  </div>
  <div class="frame">
    <div class="eyebrow">它解决的问题</div>
    <p>
      如果每个 AI 应用都要分别对接 GitHub、数据库、Figma、Notion、浏览器，集成成本会越来越高。
      <code>MCP</code> 的作用就是把这种接入方式标准化。
    </p>
    <div class="overlay-note">
      没有 MCP 时，每个产品都要自己重新造一套接外部系统的方式；有了 MCP，至少能在同一套协议上接工具、资料和模板。
    </div>
  </div>
</div>

<div class="takeaway">
  <strong>这一页要记住：</strong>
  MCP 不是 agent 本身，也不是某个单一工具；它更像一套“标准接线方式”。
</div>

<div class="source-line">
  资料：MCP 官方 Architecture 文档；Anthropic Claude Code 的 MCP 文档。
</div>

---
class: diagram-slide
---

<div class="image-frame full-diagram">
  <img src="/generated-images/mcp-primitives.png" alt="MCP 里最重要的 3 个原语" />
</div>

---
class: title-compact page-tight
---

# MCP 解决的不是“有没有工具”，而是“怎么接得标准”

<div class="split-2">
  <div class="frame">
    <div class="eyebrow">没有统一协议时</div>
    <ul class="wide-list">
      <li>每个 agent 产品都要单独适配每个外部系统</li>
      <li>工具、资料、提示模板散落在不同接入代码里</li>
      <li>换一个产品，很多集成要重新写一遍</li>
      <li>团队很难复用同一套接入方式</li>
    </ul>
  </div>
  <div class="frame accent-panel">
    <div class="eyebrow">有 MCP 之后</div>
    <ul class="wide-list">
      <li>外部系统按同一套协议暴露能力</li>
      <li>agent client 按统一方式发现并调用能力</li>
      <li>资料、动作、提示模板有了清楚的分类</li>
      <li>同一个 server 可以服务多个 agent 产品</li>
    </ul>
  </div>
</div>

<div class="takeaway">
  <strong>教学重点：</strong>
  MCP 的价值不是多一个“插件市场”，而是把 agent 和外部系统之间的接线方式标准化。
</div>

---
class: title-compact page-tight
---

# MCP client、server、外部系统怎么配合

<div class="connector-flow">
  <div class="flow-card accent-panel">
    <div class="eyebrow">Agent / Client</div>
    <h3>提出需求</h3>
    <p>例如：帮我查这个设计组件的属性，或者创建一个 GitHub issue。</p>
  </div>
  <div class="flow-line">→</div>
  <div class="flow-card">
    <div class="eyebrow">MCP Server</div>
    <h3>翻译成标准接口</h3>
    <p>把外部系统能看的资料、能做的动作、可复用的 prompt 暴露出来。</p>
  </div>
  <div class="flow-line">→</div>
  <div class="flow-card">
    <div class="eyebrow">External System</div>
    <h3>真正完成操作</h3>
    <p>例如 Figma、Notion、数据库、GitHub、浏览器或内部业务系统。</p>
  </div>
</div>

<div class="overlay-note">
  可以把 MCP server 理解成“agent 和外部系统之间的适配层”：它不替代外部系统，也不替代 agent，而是让两边按稳定协议对话。
</div>

<div class="takeaway">
  对非技术同事来说，理解到这里就够了：MCP 让 agent 接系统时更像“插标准接口”，而不是每次临时拉电线。
</div>

---

# 一个 MCP server 在真实工作里长什么样

<div class="split-2">
  <div class="frame accent-panel">
    <div class="eyebrow">例子：把设计系统接给 agent</div>
    <ul class="wide-list">
      <li><strong>Resources</strong>：提供组件文档、变量表、设计规范</li>
      <li><strong>Tools</strong>：查询某个组件支持哪些属性、获取某个页面的设计数据</li>
      <li><strong>Prompts</strong>：提供“把 Figma 设计解释成前端实现建议”的模板</li>
    </ul>
  </div>
  <div class="frame">
    <div class="eyebrow">结果会发生什么</div>
    <p>
      这时 agent 不用再靠“猜”设计系统长什么样，
      而是能通过标准接口直接读取资料、调用能力、按约定格式工作。
    </p>
    <div class="overlay-note">
      所以 MCP 的价值，不是让 agent 更聪明，而是让它接外部世界时更统一、更可复用。
    </div>
  </div>
</div>

<div class="takeaway">
  <strong>课堂例子：</strong>
  “把 Figma、Notion、数据库、浏览器统一接给 agent” 这类问题，正是 MCP 最擅长解决的。
</div>

---

# 什么时候值得接一个 MCP server

<div class="checklist">
  <div class="check-item"><div class="check-mark">1</div><div><strong>这个系统你会反复接入</strong>：不是一次性脚本，而是长期要用。</div></div>
  <div class="check-item"><div class="check-mark">2</div><div><strong>资料和动作都很多</strong>：既要读资料，又要执行操作，手写零散脚本会越来越乱。</div></div>
  <div class="check-item"><div class="check-mark">3</div><div><strong>多个 agent / 多个产品都要接</strong>：你不想每换一个 agent 产品就重写一次接入层。</div></div>
  <div class="check-item"><div class="check-mark">4</div><div><strong>你想把接入方式标准化</strong>：希望工具、资料、提示模板都能按统一方式暴露出来。</div></div>
</div>

<div class="takeaway">
  <strong>反过来说：</strong>
  如果只是一次性调用某个简单 API，往往直接写 tool 就够了，不一定非要上 MCP。
</div>

---

<div class="image-frame full-diagram">
  <img src="/generated-images/skill-pack.png" alt="Skill Pack 包含触发条件、步骤说明、示例、输出标准、注意事项、脚本和资料" />
</div>

<div class="takeaway">
  Tool 是“给 agent 一只手”，Skill 是“教 agent 一套手法”。
</div>

<div class="source-line">
  资料：Anthropic《Equipping agents for the real world with Agent Skills》；LangChain Deep Agents Skills 文档。
</div>

---
class: title-compact page-tight
---

# Skill 被调用时，agent 实际上多了一套工作流程

<div class="connector-flow">
  <div class="flow-card">
    <div class="eyebrow">1. 识别任务类型</div>
    <h3>这像哪类工作</h3>
    <p>例如做表格、改 PPT、审前端页面、处理 PDF。</p>
  </div>
  <div class="flow-line">→</div>
  <div class="flow-card accent-panel">
    <div class="eyebrow">2. 读取 Skill</div>
    <h3>按既定方法做</h3>
    <p>查看 <code>SKILL.md</code>、参考资料、模板和工具约束。</p>
  </div>
  <div class="flow-line">→</div>
  <div class="flow-card">
    <div class="eyebrow">3. 执行并验证</div>
    <h3>交付可检查结果</h3>
    <p>调用脚本、生成文件、截图检查、运行测试或给出风险说明。</p>
  </div>
</div>

<div class="takeaway">
  <strong>一句话：</strong>
  prompt 是“这次你怎么答”，skill 是“以后遇到这类任务，你都按这套流程做”。
</div>

---

# Skill 和 Prompt、Tool、Memory 的区别

<table>
  <thead>
    <tr>
      <th>概念</th>
      <th>它主要解决什么</th>
      <th>一句话理解</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>Prompt</code></td>
      <td>当下这一步怎么说清楚</td>
      <td>告诉模型这次该怎么回答</td>
    </tr>
    <tr>
      <td><code>Tool</code></td>
      <td>让 agent 能执行某个动作</td>
      <td>给它一只手</td>
    </tr>
    <tr>
      <td><code>Skill</code></td>
      <td>把一整套做事方法打包复用</td>
      <td>教它一套手法</td>
    </tr>
    <tr>
      <td><code>Memory</code></td>
      <td>让系统记住过去发生过什么</td>
      <td>让它别每次都从零开始</td>
    </tr>
  </tbody>
</table>

<div class="takeaway">
  <strong>课堂重点：</strong>
  Skill 之所以值得单独讲，是因为它不是单点功能，而是“经验、资料、脚本、规范”的打包体。
</div>

---
class: title-compact page-tight
---

# 真实工作里，一个 Skill 长什么样

<div class="split-2">
  <div class="frame accent-panel">
    <div class="eyebrow">例子：修前端页面视觉问题</div>
    <ul class="wide-list">
      <li><code>SKILL.md</code>：规定先截图、再找组件、再改样式、最后回归验证</li>
      <li>scripts：自动跑构建、截图、对比差异</li>
      <li>docs：项目里的设计规范、命名规则、组件约束</li>
    </ul>
  </div>
  <div class="frame">
    <div class="eyebrow">为什么这比一段 prompt 强</div>
    <ul class="wide-list">
      <li>prompt 只说“这次怎么做”</li>
      <li>skill 把“以后每次都怎么做”固化下来</li>
      <li>新 agent 来了也能复用，不必每次重新讲流程</li>
    </ul>
  </div>
</div>

<div class="takeaway">
  <strong>一句话：</strong>
  Skill 适合沉淀“反复出现的任务套路”，而不只是解决某一次提问。
</div>

---

# 什么时候该把 prompt 升级成 skill

<div class="split-2">
  <div class="frame">
    <div class="eyebrow">继续用 prompt 就够</div>
    <ul class="wide-list">
      <li>这是一次性任务</li>
      <li>步骤很短</li>
      <li>不需要脚本和资料包</li>
      <li>下次大概率不会再用</li>
    </ul>
  </div>
  <div class="frame accent-panel">
    <div class="eyebrow">应该升级成 skill</div>
    <ul class="wide-list">
      <li>同类任务反复出现</li>
      <li>你总在重复讲同一套要求</li>
      <li>任务依赖文档、脚本、模板、规则</li>
      <li>你希望团队里不同 agent 都按同一套套路做事</li>
    </ul>
  </div>
</div>

<div class="takeaway">
  <strong>课堂判断：</strong>
  当“怎么做”开始稳定重复时，就不该只靠 prompt 记忆了，而该把它升级成 skill。
</div>

---

# Memory：为什么 agent 不能每一轮都失忆

<div class="split-3">
  <div class="term-card">
    <h3>短期状态</h3>
    <p>这次任务当前的消息、步骤、中间结果。</p>
  </div>
  <div class="term-card">
    <h3>长期记忆</h3>
    <p>用户偏好、项目约定、反复用到的知识。</p>
  </div>
  <div class="term-card accent-panel">
    <h3>工作记忆</h3>
    <p>本轮任务生成的摘要、研究结论、临时记录。</p>
  </div>
</div>

<div class="takeaway">
  <strong>一句话：</strong>
  <code>State</code> 更像为了把这次任务做完，<code>Memory</code> 更像为了让下一次做得更好。
</div>

<div class="source-line">
  资料：Anthropic Claude Code Memory 文档；LangChain Long-term Memory 文档。
</div>

---

# 如果没有 Memory，agent 会怎么犯傻

<div class="split-2">
  <div class="frame">
    <div class="eyebrow">没有 memory 的典型表现</div>
    <ul class="wide-list">
      <li>上一轮已经确认过的约束，下一轮又忘了</li>
      <li>同一个项目约定，今天遵守、明天又偏掉</li>
      <li>每次都要重新解释目录结构、接口背景、命名规则</li>
      <li>刚做完的调研结论，下一步无法被稳定继承</li>
    </ul>
  </div>
  <div class="frame accent-panel">
    <div class="eyebrow">有 memory 之后</div>
    <ul class="wide-list">
      <li>项目约定可以持续生效</li>
      <li>用户偏好可以跨会话保留</li>
      <li>中间结论可以沉淀成下一轮的起点</li>
      <li>agent 不必每次都从“重新认识你”开始</li>
    </ul>
  </div>
</div>

<div class="takeaway">
  <strong>课堂例子：</strong>
  你第一次告诉 agent “这个仓库统一用 pnpm、测试用 vitest、不要改 generated 文件”，以后就不该每次从零再说一遍。
</div>

---

# Subagents：为什么一个 agent 还要再拆小助手

<div class="split-2">
  <div class="frame">
    <div class="eyebrow">为什么要拆</div>
    <ul class="wide-list">
      <li>主 agent 的上下文太杂</li>
      <li>某个子任务很专业</li>
      <li>想把不同任务并行化</li>
      <li>想隔离权限和工具范围</li>
    </ul>
  </div>
  <div class="frame accent-panel">
    <div class="eyebrow">拆了以后有什么好处</div>
    <ul class="wide-list">
      <li>上下文更干净</li>
      <li>专门任务成功率更高</li>
      <li>结果更容易汇总</li>
      <li>主 agent 不用记住所有细节</li>
    </ul>
  </div>
</div>

<div class="takeaway">
  <strong>教学重点：</strong>
  Subagent 的第一价值，不是“更炫”，而是 <strong>context isolation</strong>，也就是上下文隔离。
</div>

<div class="source-line">
  资料：Anthropic Claude Code Subagents 文档；LangChain Deep Agents Subagents 文档。
</div>

---
class: diagram-slide
---

<div class="image-frame full-diagram">
  <img src="/generated-images/subagents-task-split.png" alt="主 agent 将复杂任务拆给调研、实现修复和验证子 agent，并保持上下文隔离" />
</div>

---

# 把这些能力组合起来，才像今天的 agent

<div class="card-grid">
  <div class="compare-card">
    <h3>模型</h3>
    <p>负责理解需求、判断下一步。</p>
  </div>
  <div class="compare-card">
    <h3>Tools</h3>
    <p>终端、文件、浏览器、API。</p>
  </div>
  <div class="compare-card">
    <h3>MCP</h3>
    <p>把外部系统接进来。</p>
  </div>
  <div class="compare-card">
    <h3>Skills</h3>
    <p>沉淀领域做法和固定套路。</p>
  </div>
  <div class="compare-card">
    <h3>Memory</h3>
    <p>保存上下文、项目约定和历史经验。</p>
  </div>
  <div class="compare-card accent-panel">
    <h3>Subagents</h3>
    <p>把调研、实现、检查拆给不同角色。</p>
  </div>
</div>

<div class="takeaway">
  <strong>这一页要记住：</strong>
  今天常见的 agent 看起来很强，往往不是因为模型突然无所不能，而是因为这些能力层终于被接到一起了。
</div>

---
class: title-compact page-tight
---

# 只能优先补 4 层能力时，先补什么

<div class="step-grid-2 compact-step">
  <div class="step-list">
  <div class="step-item">
    <h3>先补 Tools</h3>
    <p>如果 agent 连文件、终端、网页都碰不到，再聪明也只能停在“说”。</p>
  </div>
  <div class="step-item">
    <h3>再补 Retrieval / RAG</h3>
    <p>如果它看不到项目文档、知识库、接口说明，就会大量依赖猜测。</p>
  </div>
  <div class="step-item">
    <h3>然后补 Memory / Rules</h3>
    <p>如果不能保留约定和历史结论，它每一轮都会像重新入职一样。</p>
  </div>
  </div>
  <div class="step-list" style="counter-reset: step 3;">
  <div class="step-item">
    <h3>最后再补 Skills / Subagents</h3>
    <p>当任务开始重复、分工开始复杂时，再把方法沉淀和角色拆分补上。</p>
  </div>
  </div>
</div>

<div class="takeaway">
  <strong>学生版记忆法：</strong>
  先让它能做，再让它能看，再让它能记，最后让它能复用和分工。
</div>
