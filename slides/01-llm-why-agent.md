---
class: section-dark
---

<div class="center-stage">
  <div>
    <div class="section-mark">Part 1</div>
    <div class="divider-line"></div>
    <h1 class="section-title">先讲 LLM 为什么不够</h1>
    <p class="lead tight">先把地基打稳：不理解 LLM 的机制与局限，就很难理解 agent 为什么会出现。</p>
    </div>
</div>

---
class: diagram-slide
---

<div class="image-frame full-diagram">
  <img src="/generated-images/llm-next-token.png" alt="LLM 的 next-token prediction 机制图" />
</div>

---

# 这种“词语接龙”机制，为什么已经很强

<div class="split-2">
  <div class="frame">
    <div class="eyebrow">它擅长什么</div>
    <div class="checklist">
      <div class="check-item"><div class="check-mark">✓</div><div>理解语言模式与上下文关系</div></div>
      <div class="check-item"><div class="check-mark">✓</div><div>生成结构化文本和代码</div></div>
      <div class="check-item"><div class="check-mark">✓</div><div>做局部推理、归纳和重写</div></div>
    </div>
  </div>
  <div class="frame accent-panel">
    <div class="eyebrow">但这不等于什么</div>
    <div class="checklist">
      <div class="check-item"><div class="check-mark">!</div><div>不等于它天然会操作外部世界</div></div>
      <div class="check-item"><div class="check-mark">!</div><div>不等于它天然能维护长期状态</div></div>
      <div class="check-item"><div class="check-mark">!</div><div>不等于它天然能把一件事从头做到尾</div></div>
    </div>
  </div>
</div>

<div class="takeaway">
  <strong>关键认识：</strong>
  LLM 很强，但它的强项主要在“生成与判断”，不是“执行与控制”。
</div>

---

# 最早的 chatbot，天花板在哪里

<div class="split-2">
  <div class="image-frame">
    <img src="/products/chatgpt.webp" alt="Web chat example" />
  </div>
  <div class="frame">
    <div class="eyebrow">如果产品形态只是聊天窗口</div>
    <ul class="wide-list">
      <li>它可以回答你，但不会自己继续下一步</li>
      <li>它可以建议你怎么做，但不会替你真正执行</li>
      <li>它可以给方案，但不会维护任务状态</li>
      <li>它可以生成答案，但不会验证结果是否真的成立</li>
    </ul>
    <div class="takeaway">
      chatbot 更像“回答器”，不是“任务执行器”。
    </div>
  </div>
</div>

---
class: diagram-slide
---

<div class="image-frame full-diagram">
  <img src="/generated-images/from-chat-to-agent.png" alt="从聊天到 Agent：接入环境与工具后推进任务" />
</div>

---

# Agent 是什么，不是什么

<div class="definition-grid">
  <div class="compare-card">
    <h3>Chatbot</h3>
    <p>核心任务是回答问题。</p>
    <p class="tiny muted">重点是自然语言交互。</p>
    <img src="/products/chatgpt-desktop-app.avif" alt="a" />
  </div>
  <div class="compare-card">
    <h3>Workflow</h3>
    <p>核心任务是按预先写好的流程走。</p>
    <p class="tiny muted">重点是流程可控、路径固定。</p>
    <img src="/products/n8n.png" alt="b" />
  </div>
  <div class="compare-card accent-panel">
    <h3>Agent</h3>
    <p>核心任务是围绕目标持续判断、调用工具、推进多步任务。</p>
    <p class="tiny muted">重点是动态决策与任务闭环。</p>
    <img src="/products/claude-code.webp" alt="c" />
  </div>
</div>


<div class="takeaway">
  <strong>一句话：</strong>
  Chatbot 负责回答，Workflow 负责按图执行，Agent 负责在不确定环境里推进任务。
</div>

---
class: diagram-slide
---

<div class="image-frame full-diagram">
  <img src="/generated-images/llm-inside-agent-system.png" alt="Agent 是承载 LLM、工具、状态、运行时和权限规则的软件系统" />
</div>

---
class: diagram-slide
---

<div class="image-frame full-diagram">
  <img src="/generated-images/react-agent-loop.png" alt="ReAct：Reason、Act、Observe 构成 Agent 工作闭环" />
</div>

---
class: title-compact page-tight
---

# 为什么 Agent 比最早的 chatbot 强很多

<div class="agent-upgrade">
  <div class="upgrade-baseline">
    <div class="eyebrow">早期 chatbot 的边界</div>
    <h3>一次对话，一次回答</h3>
    <p>模型只看到用户发来的文本，然后生成下一段文本。它可以建议你怎么做，但任务真正发生在哪里、做到哪一步、结果是否成功，通常都不在系统控制里。</p>
    <div class="limit-list">
      <div>纯聊天窗口，缺乏普通软件的运行环境</div>
      <div>没有远程或本地工具可供调用</div>
      <div>不知道你处理任务进展状态</div>
    </div>
  </div>

  <div class="upgrade-stack">
    <div class="upgrade-row">
      <div class="upgrade-index">01</div>
      <div>
        <strong>Runtime（运行时 / 执行环境）</strong>
        <p>这是 agent 程序真正跑起来的环境：启动会话、加载模型与工具配置、管理一次运行中的上下文 / 日志，并执行已授权的工具调用。</p>
      </div>
    </div>
    <div class="upgrade-row">
      <div class="upgrade-index">02</div>
      <div>
        <strong>Tool Use（工具调用）</strong>
        <p>模型不只输出建议，而是提出要求执行特定动作(function call, mcp)；agent(身体)收到llm（大脑）的要求，去调用互联网搜索、文件读写、浏览器控制、数据库连接、Shell 等工具。Shell 是最强大执行工具(调用操作系统命令)，但是Shell不等于 Runtime。</p>
      </div>
    </div>
    <div class="upgrade-row">
      <div class="upgrade-index">04</div>
      <div>
        <strong>Observe / Feedback Loop</strong>
        <p>每次执行都会产生反馈：命令输出、页面状态、测试结果、报错信息。下一步行动依据建立在以上证据上，而不只是猜测。</p>
      </div>
    </div>
    <div class="upgrade-row">
      <div class="upgrade-index">03</div>
      <div>
        <strong>State / Memory</strong>
        <p>任务计划、中间产物、已尝试方案、环境约束会被保留下来，所以多轮推进不是每次从零开始。</p>
      </div>
    </div>
  </div>
</div>

<div class="takeaway">
  <strong>关键区别：</strong>
  Chatbot 停在“生成答案”；Agent 把 LLM 放进一个有运行环境、有工具调用、有状态记录、有反馈的任务闭环里。
</div>

---
class: diagram-slide
---

<div class="image-frame full-diagram">
  <img src="/generated-images/shell-access-boundary.png" alt="Shell 执行能力扩展 Agent 的能力边界" />
</div>
