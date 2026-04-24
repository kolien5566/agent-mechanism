---
class: section-dark
---

<div class="center-stage">
  <div>
    <div class="section-mark">Part 2</div>
    <div class="divider-line"></div>
    <h1 class="section-title">市面上常见的 Agent 产品</h1>
    <p class="lead tight">这一章单独讲产品形态、能力边界和上手方式，重点会放在 Codex 上，后面也方便直接插入演示视频。</p>
  </div>
</div>

---

# 市面上的 Agent 产品为什么长得完全不一样

<div class="product-grid">
  <div class="product-card">
    <img src="/products/claude-code.webp" alt="Claude Code" />
    <div class="caption">
      <strong>Claude Code</strong>
      <div class="tiny">CLI / terminal 入口</div>
    </div>
  </div>
  <div class="product-card">
    <img src="/products/codex.webp" alt="Codex" />
    <div class="caption">
      <strong>Codex</strong>
      <div class="tiny">GUI / app 入口</div>
    </div>
  </div>
  <div class="product-card">
    <img src="/products/cursor.webp" alt="Cursor" />
    <div class="caption">
      <strong>Cursor</strong>
      <div class="tiny">IDE 内嵌入口</div>
    </div>
  </div>
  <div class="product-card">
    <img src="/products/openclaw-chatbot.png" alt="OpenClaw" />
    <div class="caption">
      <strong>OpenClaw</strong>
      <div class="tiny">Web chat / backend 入口</div>
    </div>
  </div>
  <div class="product-card">
    <img src="/products/n8n.png" alt="n8n" />
    <div class="caption">
      <strong>n8n</strong>
      <div class="tiny">workflow / automation 入口</div>
    </div>
  </div>
</div>

<div class="takeaway">
  Agent 不一定长成聊天窗口。终端、桌面、IDE、网页、流程画布都可以是它的外壳。
</div>

---

# 不同产品背后，其实是同一个 Agent 内核

<div class="stack">
  <div class="stack-layer accent-panel">
    <div class="layer-title">UI / Surface（交互外壳）</div>
    <div>CLI、桌面、IDE、Web、workflow canvas</div>
  </div>
  <div class="stack-layer">
    <div class="layer-title">Runtime / Harness（运行时 / 执行框架）</div>
    <div>系统怎么真正跑起来，怎么接任务、怎么继续执行、怎么接住反馈。</div>
  </div>
  <div class="stack-layer">
    <div class="layer-title">Model（模型）</div>
    <div>负责理解输入、生成输出、做局部判断。</div>
  </div>
  <div class="stack-layer">
    <div class="layer-title">Tools + State / Memory</div>
    <div>工具负责做事，状态和记忆负责把任务跨步骤延续下去。</div>
  </div>
</div>

<div class="takeaway">
  很多 Agent 产品的真正差异，其实在外壳和接入方式，而不在核心运行机制。
</div>

---

# Claude Code：它为什么一上来就显得很强

<div class="split-2">
  <div class="image-frame">
    <img src="/products/claude-code.webp" alt="Claude Code screenshot" />
  </div>
  <div class="frame">
    <div class="eyebrow">Anthropic 官方描述的核心能力</div>
    <ul class="wide-list">
      <li>读整个代码库</li>
      <li>编辑文件</li>
      <li>运行命令</li>
      <li>接入开发工具</li>
      <li>用 <code>MCP</code> 连接外部系统</li>
      <li>用 <code>CLAUDE.md</code>、memory、hooks、subagents 扩展行为</li>
    </ul>
    <div class="source-line">
      资料：Claude Code Overview、Memory、MCP、Subagents 官方文档。
    </div>
  </div>
</div>

---

# Claude Code 的能力边界：能做什么，不能做什么

<div class="split-2">
  <div class="frame accent-panel">
    <div class="eyebrow">它擅长交给 agent 的任务</div>
    <ul class="wide-list">
      <li>探索陌生代码库</li>
      <li>修 bug、补测试、重构小模块</li>
      <li>重复性的开发杂活</li>
      <li>把多个工具串起来完成一个小闭环</li>
    </ul>
  </div>
  <div class="frame">
    <div class="eyebrow">不该期待它自动解决的事</div>
    <ul class="wide-list">
      <li>替你决定高风险产品方向</li>
      <li>在模糊需求下直接给出完美架构</li>
      <li>在缺少上下文时稳定完成大型改造</li>
      <li>不经检查就保证所有修改都正确</li>
    </ul>
  </div>
</div>

<div class="takeaway">
  <strong>学生版理解：</strong>
  Claude Code 很强，但它最强的是“把明确目标变成可执行步骤”，不是“无上下文地替你当 CTO”。
</div>

---

# Codex：它为什么像一个“多 agent 指挥台”

<div class="split-2">
  <div class="image-frame">
    <img src="/products/codex.webp" alt="Codex screenshot" />
  </div>
  <div class="frame">
    <div class="eyebrow">OpenAI 官方描述的核心能力</div>
    <ul class="wide-list">
      <li>写代码、读代码、审代码、修问题</li>
      <li>完成 feature、refactor、migration</li>
      <li>支持 skills、subagents、automations</li>
      <li>支持 app、IDE、CLI、web 多种 surface</li>
      <li>强调 parallel work、background work、always-on work</li>
    </ul>
    <div class="source-line">
      资料：OpenAI Codex 产品页与 Developers 文档。
    </div>
  </div>
</div>

---

# Codex 的能力边界：什么时候它最有价值

<div class="split-2">
  <div class="frame accent-panel">
    <div class="eyebrow">适合</div>
    <ul class="wide-list">
      <li>任务可以拆成多个并行工作块</li>
      <li>你希望 agent 在后台持续推进</li>
      <li>你需要 review、diff、workspace、task view 这些“工作台能力”</li>
      <li>你想把 agent 作为团队协作系统的一部分</li>
    </ul>
  </div>
  <div class="frame">
    <div class="eyebrow">不适合</div>
    <ul class="wide-list">
      <li>你根本还没想清楚要做什么</li>
      <li>需求和上下文都极度模糊</li>
      <li>不愿意给规则、不给反馈、也不做验收</li>
      <li>期待“一句自然语言就自动交付完整产品”</li>
    </ul>
  </div>
</div>

<div class="takeaway">
  Codex 的亮点不是“更像聊天框”，而是它把多任务、多环境、多 agent 协作组织成了一个工作台。
</div>

---
class: title-compact page-tight
---

# 明天就开始用 Claude Code / Codex：6 条最实用规则

<div class="rule-mosaic">
  <div class="rule-card">
    <div class="rule-no">1</div>
    <h3>先给目标，不要先给实现细节</h3>
    <p>先说“我要什么结果”，再补“有哪些约束”。</p>
  </div>
  <div class="rule-card">
    <div class="rule-no">2</div>
    <h3>把上下文喂够，但别喂垃圾</h3>
    <p>给目录、文件、报错、日志、接口说明，不要把无关内容一股脑倒进去。</p>
  </div>
  <div class="rule-card">
    <div class="rule-no">3</div>
    <h3>让它先探索，再动手</h3>
    <p>尤其是陌生代码库，先让它读、搜、总结，再让它改。</p>
  </div>
  <div class="rule-card">
    <div class="rule-no">4</div>
    <h3>把任务拆小</h3>
    <p>“补测试”“修 bug”“重构某模块”都比“帮我把系统全面优化一下”更容易成功。</p>
  </div>
  <div class="rule-card">
    <div class="rule-no">5</div>
    <h3>要求验证</h3>
    <p>不要只让它改，要让它运行测试、解释结果、指出剩余风险。</p>
  </div>
  <div class="rule-card">
    <div class="rule-no">6</div>
    <h3>你仍然是负责人</h3>
    <p>agent 可以做很多执行工作，但目标定义、最终验收、关键判断仍然在你手里。</p>
  </div>
</div>

<div class="takeaway">
  <strong>一句话：</strong>
  会不会用 agent，关键不只是“会不会提问”，而是会不会给目标、上下文、约束和验收标准。
</div>

---

# 第一次把任务交给 agent 工具，可以直接照这个模板说

<div class="split-2">
  <div class="frame accent-panel">
    <div class="eyebrow">推荐模板</div>
    <p>
      先读 <code>src/auth</code> 和相关测试，定位登录失败的原因。
      只在这个目录内修改。
      修复后运行测试并总结你改了什么、还有什么风险。
    </p>
  </div>
  <div class="frame">
    <div class="eyebrow">这个模板为什么好</div>
    <ul class="wide-list">
      <li>给了目标：定位并修复登录失败</li>
      <li>给了范围：只在某个目录内修改</li>
      <li>给了动作：先读、再改、再测</li>
      <li>给了验收：说明改动和剩余风险</li>
    </ul>
  </div>
</div>

<div class="takeaway">
  <strong>实操原则：</strong>
  你给 agent 的不是“灵感”，而是一份足够清楚的任务合同。
</div>

---
class: title-compact page-tight
zoom: 0.94
---

# Claude Code、Codex、Cursor：怎么选

<table>
  <thead>
    <tr>
      <th>产品</th>
      <th>最像什么</th>
      <th>什么时候优先考虑</th>
      <th>你要注意什么</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td><code>Claude Code</code></td>
      <td>终端里的 agent</td>
      <td>你已经在 shell 和代码库里工作，想快速探索、修改、执行、验证</td>
      <td>上下文要给够，目标要清晰，不要期待它替你做高层产品判断</td>
    </tr>
    <tr>
      <td><code>Codex</code></td>
      <td>agent 工作台</td>
      <td>你想把任务拆分、并行、后台推进，或者需要更强的工作流组织能力</td>
      <td>适合任务组织，不等于需求自动清晰；仍然需要你定义目标与验收</td>
    </tr>
    <tr>
      <td><code>Cursor</code></td>
      <td>IDE 里的 agent</td>
      <td>你主要在编辑器里连续写代码，希望 AI 融入编码流程</td>
      <td>适合“边写边协作”，但复杂任务仍然需要结构化地拆开</td>
    </tr>
  </tbody>
</table>

<div class="takeaway">
  <strong>课堂判断：</strong>
  这几个产品不是“谁绝对更强”的关系，而是入口不同、工作组织方式不同、适配场景不同。
</div>

---

# 一个“适合交给 agent”的任务，应该长什么样

<div class="split-2">
  <div class="frame accent-panel">
    <div class="eyebrow">坏任务</div>
    <p class="mini-headline">“帮我全面优化一下这个项目。”</p>
    <ul class="wide-list">
      <li>目标模糊</li>
      <li>边界不清</li>
      <li>没有上下文</li>
      <li>没有验收标准</li>
    </ul>
  </div>
  <div class="frame">
    <div class="eyebrow">好任务</div>
    <p class="mini-headline">“先读这个目录，定位登录报错原因，修复后跑测试并解释改动。”</p>
    <ul class="wide-list">
      <li>目标明确</li>
      <li>范围清楚</li>
      <li>上下文可给</li>
      <li>结果能验证</li>
    </ul>
  </div>
</div>

<div class="takeaway">
  <strong>一句话：</strong>
  越像“明确目标 + 限定范围 + 可验证结果”的任务，越适合交给 agent。
</div>

---

# 新手最容易犯的 5 个错误

<div class="checklist">
  <div class="check-item"><div class="check-mark">1</div><div><strong>把 agent 当搜索框用</strong>：结果只会停留在“会说”，而不是“会做”。</div></div>
  <div class="check-item"><div class="check-mark">2</div><div><strong>目标过大</strong>：一句“帮我重构系统”通常不会有好结果。</div></div>
  <div class="check-item"><div class="check-mark">3</div><div><strong>不给上下文</strong>：不给目录、错误信息、文件路径，等于让它在黑暗里猜。</div></div>
  <div class="check-item"><div class="check-mark">4</div><div><strong>不让它验证</strong>：改完不跑测试、不看输出，成功率会明显下降。</div></div>
  <div class="check-item"><div class="check-mark">5</div><div><strong>把 agent 当绝对权威</strong>：它是执行助手，不是免审查的最终负责人。</div></div>
</div>

<div class="takeaway">
  这 5 个错误，本质上都指向同一件事：你没有把 agent 当作“软件系统”，而是当成“更高级的聊天框”。
</div>
