---
class: section-dark
---

<div class="center-stage">
  <div>
    <div class="section-mark">Part 1</div>
    <div class="divider-line"></div>
    <h1 class="section-title">先讲 LLM 为什么不够</h1>
    <p class="lead tight">先把地基打稳：不理解 LLM 的机制与局限，就很难真正理解 agent 为什么会出现。</p>
  </div>
</div>

---
class: diagram-slide
---

<div class="image-frame full-diagram">
  <img src="/generated-images/llm-next-token.png" alt="LLM 的 next-token prediction 机制图" />
</div>

<div class="source-line">
  资料：OpenAI 官方模型与推理文档；Anthropic 关于 agent 与 context engineering 的官方文章。
</div>

---

# 这种“词语接龙”机制，为什么已经很强

<div class="split-2">
  <div class="frame">
    <div class="eyebrow">它擅长什么</div>
    <div class="checklist">
      <div class="check-item"><div class="check-mark">✓</div><div>理解语言模式与上下文关系</div></div>
      <div class="check-item"><div class="check-mark">✓</div><div>生成结构化文本和代码</div></div>
      <div class="check-item"><div class="check-mark">✓</div><div>模仿格式、风格、例子</div></div>
      <div class="check-item"><div class="check-mark">✓</div><div>做局部推理、归纳和重写</div></div>
    </div>
  </div>
  <div class="frame accent-panel">
    <div class="eyebrow">但这不等于什么</div>
    <div class="checklist">
      <div class="check-item"><div class="check-mark">!</div><div>不等于它天然会执行任务</div></div>
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

# 最早的 chatbot，天花板到底在哪里

<div class="split-2">
  <div class="image-frame">
    <img src="/products/openclaw-chatbot.png" alt="Web chat example" />
  </div>
  <div class="frame">
    <div class="eyebrow">如果系统形态只是聊天窗口</div>
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

# Agent 到底是什么，不是什么

<div class="definition-grid">
  <div class="compare-card">
    <h3>Chatbot</h3>
    <p>核心任务是回答问题。</p>
    <p class="tiny muted">重点是自然语言交互。</p>
  </div>
  <div class="compare-card">
    <h3>Workflow</h3>
    <p>核心任务是按预先写好的流程走。</p>
    <p class="tiny muted">重点是流程可控、路径固定。</p>
  </div>
  <div class="compare-card accent-panel">
    <h3>Agent</h3>
    <p>核心任务是围绕目标持续判断、调用工具、推进多步任务。</p>
    <p class="tiny muted">重点是动态决策与任务闭环。</p>
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

# 为什么 Agent 比最早的 chatbot 强很多

<div class="tool-grid">
  <div class="tool-tile"><strong>Runtime</strong>让系统持续运行，而不是只回答一次。</div>
  <div class="tool-tile"><strong>Tool Use</strong>让模型能接触外部能力，而不是困在文本里。</div>
  <div class="tool-tile"><strong>State / Memory</strong>让任务可以跨步骤推进，而不是每轮都重新开始。</div>
  <div class="tool-tile"><strong>Observe</strong>让下一步建立在真实反馈上，而不是只靠猜。</div>
</div>

<div class="split-2" style="margin-top:1rem;">
  <div class="image-frame">
    <img src="/products/claude-code.webp" alt="Claude Code screenshot" />
  </div>
  <div class="frame accent-panel">
    <h3>看图理解</h3>
    <p>当系统已经能读代码、跑命令、看输出、继续下一步时，它就不只是聊天窗口了，而是在真实环境里工作。</p>
    <div class="takeaway">
      chatbot 更像回答器，agent 更像任务执行系统。
    </div>
  </div>
</div>

---
class: diagram-slide
---

<div class="image-frame full-diagram">
  <img src="/generated-images/shell-access-boundary.png" alt="Shell 执行能力扩展 Agent 的能力边界" />
</div>
