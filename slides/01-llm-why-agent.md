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
    <img src="/products/chatgpt.png" alt="Web chat example" />
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
class: title-compact page-tight
---

# Agent 是什么

<p class="lead tight">
Agent 是一种 AI 应用软件：LLM 参与控制运行过程，而不只是生成一段回答。
</p>

<div class="definition-grid">
  <div class="compare-card">
    <h3>先理解软件</h3>
    <p>软件不是屏幕上的界面，而是一组会被计算机执行的程序、数据和规则。</p>
    <p class="tiny muted">运行起来以后，它会接收输入、读写状态、调用系统能力或外部 API，并产生输出。</p>
  </div>
  <div class="compare-card">
    <h3>LLM 不是全部</h3>
    <p>LLM 负责根据上下文判断“下一步应该做什么”。</p>
    <p class="tiny muted">但读文件、联网、调 Shell、保存任务进度、控制权限，都要由外层软件来完成。</p>
  </div>
  <div class="compare-card accent-panel">
    <h3>Agent 的本质</h3>
    <p>把 LLM 的判断接到真实的软件能力上，让它参与任务的执行流程。</p>
    <p class="tiny muted">所以 Agent 至少要有上下文、工具接口、状态记录、权限边界和结束条件。</p>
  </div>
</div>


<div class="takeaway">
  <strong>一句话：</strong>
  Agent 的关键不是“更会聊天”，而是把 LLM 放进一个真实运行的软件系统里，让模型参与决定这个软件接下来要调用什么能力、观察什么结果、什么时候结束任务。
</div>

---
class: title-compact page-tight
---

# Agent 不是什么

<p class="lead tight">
Chatbot、Workflow 和 Agent 都可以接入模型，但它们控制任务的方式不同。
</p>

<div class="definition-grid">
  <div class="compare-card">
    <h3>Chatbot</h3>
    <p>核心是对话界面，把用户输入转成一段回答。</p>
    <p class="tiny muted">通常停在“请求 → 回复”，不负责持续维护任务状态。</p>
    <img src="/products/chatgpt.png" alt="ChatGPT 对话产品截图" />
  </div>
  <div class="compare-card">
    <h3>Workflow</h3>
    <p>核心是预先写好的流程编排，按固定节点和分支执行。</p>
    <p class="tiny muted">路径主要由人提前设计，遇到没写进流程的情况不会自己改策略。</p>
    <img src="/products/n8n.png" alt="n8n workflow 产品截图" />
  </div>
  <div class="compare-card accent-panel">
    <h3>Agent</h3>
    <p>核心是在运行中判断下一步，调用工具，观察结果，再继续推进。</p>
    <p class="tiny muted">路径不是完全写死的，而是由模型在软件约束下动态选择。</p>
    <img src="/products/claude-code.webp" alt="Claude Code agent 产品截图" />
  </div>
</div>

<div class="takeaway">
  <strong>区别：</strong>
  Chatbot 主要负责回答，Workflow 主要负责按图执行，Agent 主要负责在不确定环境里持续决策和行动。
</div>

---
class: diagram-slide
---

<div class="image-frame full-diagram">
  <img src="/generated-images/llm-inside-agent-system.png" alt="Agent 是承载 LLM、工具、状态、运行时和权限规则的软件系统" />
</div>

---
class: title-compact page-tight mechanism-slide
---

# Agent Loop：Agent 的最小工作模式

<p class="lead tight">也被称为 ReAct 模式：不是一次性回答，而是在“思考、行动、观察”之间反复推进，直到任务完成。</p>

<div class="mechanism-layout">
  <div class="image-frame mechanism-diagram">
    <img src="/generated-images/agent-loop.png" alt="Agent Loop：模型反复思考、调用工具、观察结果，并在完成后输出 Final Answer" />
  </div>

  <div class="frame mechanism-copy">
    <div class="eyebrow">Agent Loop / ReAct</div>
    <h3>从“回答问题”变成“推进任务”</h3>
    <p>初始需求把任务交给 Agent。真正的循环从“思考下一步”开始。</p>
    <div class="limit-list">
      <div><strong>思考下一步</strong>：根据当前状态决定要不要调用工具。</div>
      <div><strong>执行并观察</strong>：工具返回结果后，Agent 把结果重新纳入上下文。</div>
      <div><strong>判断是否完成</strong>：未完成就继续循环；完成后才输出 Final Answer。</div>
    </div>
  </div>
</div>

<div class="takeaway">
  <strong>关键点：</strong>
  Agent 的“聪明”不只来自模型本身，还来自这个能持续行动、观察和修正的闭环。
</div>

---
class: title-compact page-tight mechanism-slide
---

# Human-in-the-loop：把人放进 Agent Loop

<p class="lead tight">当工具调用可能影响文件、账号、资金、权限或真实用户时，Agent 不应该直接执行，而是先让人审核。</p>

<div class="mechanism-layout">
  <div class="image-frame mechanism-diagram">
    <img src="/generated-images/human-in-the-loop.png" alt="Human-in-the-loop：人类在高风险工具执行前审批、修改或拒绝" />
  </div>

  <div class="frame mechanism-copy">
    <div class="eyebrow">Human-in-the-loop</div>
    <h3>人类负责审核边界</h3>
    <p>人工审核插在“准备调用工具”和“执行工具”之间，拦住真正会改变外部世界的动作。</p>
    <div class="limit-list">
      <div><strong>批准</strong>：动作继续执行，结果再回到观察与判断。</div>
      <div><strong>修改</strong>：人调整动作边界，让 Agent 回到下一步规划。</div>
      <div><strong>拒绝</strong>：危险动作不执行，Agent 重新思考替代方案。</div>
    </div>
  </div>
</div>

<div class="takeaway">
  <strong>关键点：</strong>
  Human-in-the-loop 不是降低自动化，而是在高风险步骤上加入可控的治理边界。
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
      <div>纯聊天窗口，缺乏软件的运行环境</div>
      <div>没有远程或本地工具可供调用</div>
      <div>不知道你处理任务进展状态</div>
    </div>
  </div>

  <div class="upgrade-stack">
    <div class="upgrade-row">
      <div class="upgrade-index">01</div>
      <div>
        <strong>Runtime（运行环境）</strong>
        <p>Agent 作为软件，需要运行在一个能接触外部环境的 runtime 里。这个运行环境决定它能否读写文件、联网、启动进程、或者访问远程服务。</p>
      </div>
    </div>
    <div class="upgrade-row">
      <div class="upgrade-index">02</div>
      <div>
        <strong>Tool Use（工具调用）</strong>
        <p>模型不只输出建议，而是提出要求执行特定动作(function call)；agent(身体)收到llm（大脑）的要求，去调用互联网搜索、文件读写、数据库连接、Shell 等工具。Shell 是最强大执行工具(调用操作系统命令)，但是Shell不等于 Runtime。</p>
      </div>
    </div>
    <div class="upgrade-row">
      <div class="upgrade-index">03</div>
      <div>
        <strong>State / Memory</strong>
        <p>任务计划、中间产物、已尝试方案、环境约束会被保留下来，所以多轮推进不是每次从零开始。</p>
      </div>
    </div>
    <div class="upgrade-row">
      <div class="upgrade-index">04</div>
      <div>
        <strong>Observe / Feedback Loop</strong>
        <p>每次执行都会产生反馈：命令输出、页面状态、测试结果、报错信息。下一步行动依据建立在以上证据上，而不只是猜测。</p>
      </div>
    </div>    
  </div>
</div>

<div class="takeaway">
  <strong>关键区别：</strong>
  Chatbot 停在“生成答案”；Agent 把 LLM 放进一个有运行环境、有工具调用、有状态记录、有反馈的任务闭环里。
</div>


---
class: title-compact page-tight
---

# Agent哪怕只有shell调用+前端GUI也足够强大

<div class="openclaw-showcase">
  <div class="frame accent-panel openclaw-copy">
    <div class="eyebrow">为什么这已经很强</div>
    <p>
      这意味着用户可以通过自然语言，间接控制操作系统已经提供的大量基础能力：
      文件、进程、网络请求、脚本。
    </p>
    <div class="limit-list">
      <div><strong>Shell</strong> 提供操作系统命令执行入口</div>
      <div><strong>前端 GUI</strong> 把能力包装成普通用户能用的产品</div>
      <div><strong>Agent</strong> 在中间负责理解目标、触发动作、观察结果</div>
    </div>
    <div class="takeaway">
      最近爆火的 OpenClaw就是一个直观例子，哪怕不额外挂载任何插件，软件初始就让人觉得足够好用。当然OpenClaw还有其能力拓展的方案，比如skill hub社区生态。
    </div>
  </div>

  <div class="openclaw-images">
    <div class="image-frame openclaw-shot">
      <img src="/products/openclaw-chatbot.png" alt="OpenClaw chatbot interface" />
    </div>
    <div class="image-frame openclaw-shot">
      <img src="/products/openclaw-web.avif" alt="OpenClaw web interface" />
    </div>
  </div>
</div>

---
class: diagram-slide
---

<div class="image-frame full-diagram">
  <img src="/generated-images/shell-access-boundary.png" alt="Shell 执行能力扩展 Agent 的能力边界" />
</div>
