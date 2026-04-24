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

# 为什么我们需要 Agent

<div class="split-2">
  <div class="frame">
    <div class="big-number">01</div>
    <h3>因为只会“说”还不够</h3>
    <p>真实工作里，很多任务需要查文件、跑命令、读日志、改代码、继续验证。</p>
  </div>
  <div class="frame accent-panel">
    <div class="big-number">02</div>
    <h3>因为系统必须会“做”</h3>
    <p>Agent 出现，是为了把模型接入环境、工具和状态，让它从“回答问题”升级成“推进任务”。</p>
  </div>
</div>

<div class="overlay-note">
  agent 诞生，不是因为大家想给 LLM 换个包装，而是因为仅靠 LLM 已经无法满足真实任务系统的需求。
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

# Agent 不是模型本身，而是承载模型的软件系统

<div class="split-2">
  <div class="frame">
    <div class="eyebrow">LLM 更像什么</div>
    <h3>能力引擎</h3>
    <ul class="wide-list">
      <li>负责理解输入</li>
      <li>负责生成输出</li>
      <li>负责局部判断和推理</li>
      <li>可以替换成不同模型</li>
    </ul>
  </div>
  <div class="frame accent-panel">
    <div class="eyebrow">Agent 更像什么</div>
    <h3>完整的软件程序</h3>
    <ul class="wide-list">
      <li>负责组织模型、工具、状态</li>
      <li>负责决定任务怎么持续推进</li>
      <li>负责接入环境、观察结果、继续执行</li>
      <li>负责把一整件事做完，而不是只给一句回答</li>
    </ul>
  </div>
</div>

<div class="takeaway">
  Agent 不是模型本身，而是承载模型的软件系统。换模型会影响表现，但不会改变 agent 的系统结构。
</div>

---

# ReAct：Agent 的最小工作原理

<div class="process-row">
  <div class="panel">
    <div class="eyebrow">1</div>
    <h3>Reason</h3>
    <p>先判断：现在最该做什么。</p>
  </div>
  <div class="process-arrow">→</div>
  <div class="panel accent-panel">
    <div class="eyebrow">2</div>
    <h3>Act</h3>
    <p>执行动作，或者调用工具。</p>
  </div>
  <div class="process-arrow">→</div>
  <div class="panel">
    <div class="eyebrow">3</div>
    <h3>Observe</h3>
    <p>读取结果，再决定是否继续。</p>
  </div>
</div>

<div class="tool-grid" style="margin-top:1rem;">
  <div class="tool-tile"><strong>终端</strong>运行命令、脚本、测试</div>
  <div class="tool-tile"><strong>文件</strong>读代码、改文件、看配置</div>
  <div class="tool-tile"><strong>浏览器</strong>看网页、查资料、交互验证</div>
  <div class="tool-tile"><strong>API</strong>接入系统和外部服务</div>
</div>

<div class="takeaway">
  <code>ReAct</code> 不只是“先想再答”的技巧，在现代 agent 里，它更像一个真实运行的系统循环。
</div>

<div class="source-line">
  资料：ReAct 论文；Anthropic 与 LangChain 官方 agent 文档。
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

# 为什么执行 shell 命令会极大扩展能力边界

<div class="split-2">
  <div class="frame">
    <div class="eyebrow">没有 shell 的时候</div>
    <ul class="wide-list">
      <li>只能建议“你去运行这个命令”</li>
      <li>只能说“也许应该检查这个文件”</li>
      <li>不能自己读取真实环境中的反馈</li>
    </ul>
  </div>
  <div class="frame accent-panel">
    <div class="eyebrow">有 shell access 的时候</div>
    <ul class="wide-list">
      <li>可以直接查看目录和文件</li>
      <li>可以运行测试和脚本</li>
      <li>可以查询日志和系统信息</li>
      <li>可以修改后再次执行验证</li>
      <li>可以接上现有开发工具链</li>
    </ul>
  </div>
</div>

<div class="takeaway">
  命令行执行能力让 LLM 从“文本生成器”变成“环境操作者”。
</div>
