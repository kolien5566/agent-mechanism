---
class: section-dark
---

<div class="center-stage">
  <div>
    <div class="section-mark">Part 3</div>
    <h1 class="section-title">工程重点为什么会迁移</h1>
    <p class="lead">这部分不是流行词科普，而是解释：为什么今天做 agent，光写 prompt 已经不够了。</p>
  </div>
</div>

---

# 为什么最早大家都在讲 Prompt Engineering

<div class="split-2">
  <div class="frame">
    <div class="eyebrow">早期任务长什么样</div>
    <ul class="wide-list">
      <li>问答</li>
      <li>总结</li>
      <li>改写</li>
      <li>写文案</li>
      <li>抽取信息</li>
    </ul>
  </div>
  <div class="frame accent-panel">
    <div class="eyebrow">当时最关键的问题</div>
    <ul class="wide-list">
      <li>怎么把任务说清楚</li>
      <li>怎么给示例</li>
      <li>怎么约束输出格式</li>
      <li>怎么让回答更稳定</li>
    </ul>
  </div>
</div>

<div class="takeaway">
  <strong>结论：</strong>
  <code>Prompt Engineering</code> 会先出现，是因为早期问题主要集中在“怎么提问”。
</div>

---

# 为什么演进到 Context Engineering

<div class="split-2">
  <div class="frame">
    <div class="eyebrow">任务变复杂之后</div>
    <ul class="wide-list">
      <li>变成多轮、多步</li>
      <li>接上工具与检索</li>
      <li>需要历史状态</li>
      <li>需要读取文件和环境</li>
    </ul>
  </div>
  <div class="frame accent-panel">
    <div class="eyebrow">失败原因也变了</div>
    <ul class="wide-list">
      <li>不是 prompt 不够华丽</li>
      <li>而是给错了信息</li>
      <li>或者给多了噪音</li>
      <li>或者漏掉了关键上下文</li>
    </ul>
  </div>
</div>

<div class="takeaway">
  <strong>结论：</strong>
  <code>Context Engineering</code> 真正解决的问题，是“每一步到底该给模型看什么”。
</div>

<div class="source-line">
  资料：Anthropic《Effective context engineering for AI agents》；LangChain Context Engineering 文档。
</div>

---

# 为什么 Context Engineering 还不够

<div class="frame">
  <p class="quote-block">
    当 agent 不只是聊天，而是开始真实执行任务时，问题已经不只是“怎么说”和“给它看什么”。
  </p>
</div>

<div class="tag-row">
  <div class="mini-card"><strong>真实执行</strong><div>要跑命令、调工具、改文件</div></div>
  <div class="mini-card"><strong>长任务</strong><div>要跨很多轮，还可能中断</div></div>
  <div class="mini-card"><strong>结果负责</strong><div>要检查输出是否真的正确</div></div>
</div>

<div class="takeaway">
  光有 prompt 和 context，还不足以让一整套执行系统稳定把事情做完。
</div>

---

# Harness Engineering：开始关心“系统怎么跑完整件事”

<div class="card-grid">
  <div class="compare-card">
    <h3>执行环境</h3>
    <p>系统在哪儿运行，能访问哪些工具和文件。</p>
  </div>
  <div class="compare-card">
    <h3>任务衔接</h3>
    <p>多轮任务怎么接续，中断后怎么继续。</p>
  </div>
  <div class="compare-card">
    <h3>结果检查</h3>
    <p>怎么验证刚才那一步到底做对了没有。</p>
  </div>
  <div class="compare-card">
    <h3>人工确认</h3>
    <p>关键操作要不要让人看一眼再继续。</p>
  </div>
  <div class="compare-card">
    <h3>运行记录</h3>
    <p>系统每一步做了什么，事后能不能回看。</p>
  </div>
  <div class="compare-card accent-panel">
    <h3>系统闭环</h3>
    <p>让 agent 真正从“回答器”变成“执行系统”。</p>
  </div>
</div>

<div class="takeaway">
  <strong>这一页要记住：</strong>
  <code>Harness Engineering</code> 之所以出现，是因为 agent 已经不再只是聊天程序，而是执行系统。
</div>

<div class="source-line">
  资料：OpenAI《Harness engineering: leveraging Codex in an agent-first world》；Anthropic《Harness design for long-running application development》。
</div>

---

# 为什么工程重心会从 Prompt 移到 Context，再移到 Harness

<div class="three-stage">
  <div class="stage-card">
    <div class="eyebrow">阶段 1</div>
    <h3>Prompt Engineering</h3>
    <p>核心问题：怎么把任务说清楚。</p>
  </div>
  <div class="stage-card">
    <div class="eyebrow">阶段 2</div>
    <h3>Context Engineering</h3>
    <p>核心问题：每一步该给模型看什么。</p>
  </div>
  <div class="stage-card">
    <div class="eyebrow">阶段 3</div>
    <h3>Harness Engineering</h3>
    <p>核心问题：怎么让整套系统把任务做完。</p>
  </div>
</div>

<div class="stage-bridge">
  <div class="bridge-note">任务复杂度上升：从单轮问答走向多轮、多工具、多步骤任务。</div>
  <div class="bridge-note">真实执行出现：开始接环境、跑命令、接反馈、做验证。</div>
</div>

<div class="takeaway">
  <strong>教学重点：</strong>
  这不是流行词替换，而是系统复杂度升级后，控制点一步步往外移。
</div>

---

# Agent 的发展历程：从会说，到会做，到能稳定完成任务

<table>
  <thead>
    <tr>
      <th>阶段</th>
      <th>代表能力</th>
      <th>大家最关心什么</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Chatbot 阶段</td>
      <td>问答、写作、总结</td>
      <td>回答得像不像人</td>
    </tr>
    <tr>
      <td>Tool Use 阶段</td>
      <td>调用搜索、文件、API</td>
      <td>能不能真正接触外部世界</td>
    </tr>
    <tr>
      <td>Agent 阶段</td>
      <td>多步任务、状态、反馈循环</td>
      <td>能不能自己把任务推进下去</td>
    </tr>
    <tr>
      <td>Harness 阶段</td>
      <td>长任务、执行环境、验证、协作</td>
      <td>能不能把整件事稳定做完</td>
    </tr>
  </tbody>
</table>

---

# 什么时候该用 Agent，什么时候不该用

<div class="split-2">
  <div class="frame accent-panel">
    <div class="eyebrow">适合用 agent</div>
    <ul class="wide-list">
      <li>任务要分很多步</li>
      <li>过程不完全确定</li>
      <li>需要反复查资料和操作环境</li>
      <li>需要系统自己推进，而不想人手动盯每一步</li>
    </ul>
  </div>
  <div class="frame">
    <div class="eyebrow">不适合用 agent</div>
    <ul class="wide-list">
      <li>单轮问答就够了</li>
      <li>规则已经写死</li>
      <li>流程极其固定</li>
      <li>成本和延迟要求极高，但又不需要灵活性</li>
    </ul>
  </div>
</div>

<div class="takeaway">
  <strong>结论：</strong>
  Agent 不是万能钥匙，它适合的是“不确定、多步、依赖环境交互”的任务。
</div>

---

# 总结：把这一整节课收成 5 句话

<div class="stack">
  <div class="stack-layer accent-panel">
    <div class="layer-title">1. LLM 很强，但它首先是生成系统</div>
    <div>它擅长理解与生成，不天然擅长执行与控制。</div>
  </div>
  <div class="stack-layer">
    <div class="layer-title">2. Agent 出现，是为了补足 LLM 的系统能力短板</div>
    <div>例如运行、工具、状态、环境交互、结果检查。</div>
  </div>
  <div class="stack-layer">
    <div class="layer-title">3. Agent 不是模型本身，而是承载模型的软件系统</div>
    <div>模型是部件，agent 是系统。</div>
  </div>
  <div class="stack-layer">
    <div class="layer-title">4. MCP、Skill、Memory、Subagent 都不是“噱头”</div>
    <div>它们分别在补接入、复用、记忆、分工这些系统能力。</div>
  </div>
  <div class="stack-layer">
    <div class="layer-title">5. 工程重点从 Prompt 移到 Context 再到 Harness</div>
    <div>是因为任务越来越复杂，系统越来越像真正的软件程序。</div>
  </div>
</div>

---

# 参考资料

- [Anthropic: Building effective agents](https://www.anthropic.com/engineering/building-effective-agents)
- [Anthropic: Effective context engineering for AI agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
- [Anthropic: Harness design for long-running application development](https://www.anthropic.com/engineering/harness-design-long-running-apps)
- [Anthropic Claude Code Docs](https://docs.anthropic.com/en/docs/claude-code/overview)
- [Anthropic Claude Code MCP](https://docs.anthropic.com/en/docs/claude-code/mcp)
- [Anthropic Claude Code Memory](https://docs.anthropic.com/en/docs/claude-code/memory)
- [Anthropic Claude Code Subagents](https://docs.anthropic.com/en/docs/claude-code/sub-agents)
- [Anthropic: Equipping agents for the real world with Agent Skills](https://www.anthropic.com/engineering/equipping-agents-for-the-real-world-with-agent-skills)
- [Model Context Protocol Documentation](https://modelcontextprotocol.io/docs/learn/architecture)
- [LangChain Agents](https://docs.langchain.com/oss/python/langchain/agents)
- [LangChain Deep Agents Skills](https://docs.langchain.com/oss/python/deepagents/skills)
- [LangChain Long-term Memory](https://docs.langchain.com/oss/python/langchain/long-term-memory)
- [OpenAI: Harness engineering](https://openai.com/index/harness-engineering/)

<div class="takeaway">
  这份 deck 现在已经不是提纲，而是一套可以继续精修成正式课程稿的讲义骨架。
</div>
