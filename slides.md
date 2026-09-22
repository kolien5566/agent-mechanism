---
theme: default
title: AI Agent：原理与使用
info: 面向非技术听众的通用 Agent 入门课
class: hero-slide
mdc: true
aspectRatio: 16/9
canvasWidth: 1280
duration: 90min
drawings:
  persist: false
---

<div class="hero-content">
  <div class="eyebrow">AI AGENT · 原理与使用</div>
  <h1 class="hero-title">从生成回答<br>到执行任务</h1>
  <p class="lead">模型如何使用工具、处理信息，并根据结果继续行动。</p>
  <div class="hero-topics">基本机制 <span>／</span> 产品与用法 <span>／</span> 能力扩展 <span>／</span> 工程演进</div>
</div>

<!--
课程共 90 分钟：讲解约 70 分钟、现场演示 15 分钟、交流 5 分钟。
听众的岗位不限定课程用途。例子覆盖文档、搜索、表格与文件操作，说明通用机制。
-->

---
class: access-slide
---

# 本次演示的工具接入

<p class="lead">通过 API（模型调用接口）接入模型，在 ChatGPT 桌面端演示 GPT‑6。</p>

<div class="split-3">
  <div class="term-card"><div class="eyebrow">API 服务</div><h3>PackyAPI</h3><p>提供 API 访问、令牌与用量管理。</p><a class="resource-link" href="https://packyapi.ai" target="_blank">packyapi.ai ↗</a></div>
  <div class="term-card"><div class="eyebrow">配置管理</div><h3>CC Switch</h3><p>添加供应商，管理客户端使用的连接配置。</p><a class="resource-link" href="https://github.com/farion1231/cc-switch" target="_blank">项目与下载 ↗</a></div>
  <div class="term-card accent-panel"><div class="eyebrow">任务入口</div><h3>ChatGPT 桌面端</h3><p>使用已配置的模型，读取材料并执行任务。</p><div class="demo-label">现场演示</div></div>
</div>

<p class="note">演示顺序：查看令牌与模型 → 配置供应商 → 打开客户端并测试。</p>

<!--
这一页只介绍三个工具的作用，详细操作现场展示；不把配置管理误画成必经的请求转发链路。
PackyAPI 接入：https://docs.packyapi.ai/docs/ccswitch/6-codex-app.html
供应商配置：https://docs.packyapi.ai/docs/ccswitch/3-codex.html
CC Switch：https://github.com/farion1231/cc-switch
GPT-6：https://developers.openai.com/api/docs/models/gpt-6-astra
API 接入和 ChatGPT 订阅分别计费；实际模型、客户端版本和权限以演示账号为准。提前确认链路可用，不在课件中放真实 API Key。
-->

---

# 同一个任务，三种处理方式

<p class="lead">例子：整理一个文件夹里的资料，生成一份摘要。</p>

<div class="split-3">
  <div class="compare-card"><div class="eyebrow">纯文本问答</div><h3>生成回答</h3><p>根据粘贴的材料写摘要，文件整理和后续操作由人完成。</p></div>
  <div class="compare-card"><div class="eyebrow">Workflow · 工作流</div><h3>按预设流程执行</h3><p>依次读取、分类、输出；路径由事先配置的节点和分支决定。</p></div>
  <div class="compare-card accent-panel"><div class="eyebrow">Agent · 智能体</div><h3>根据结果继续行动</h3><p>读取资料、发现缺项、补充检索，再整理输出并检查结果。</p></div>
</div>

<p class="note">实际产品可以组合这些方式；聊天窗口也可以承载 Agent。</p>

<!--
比较的是控制任务的方式，不是三个互斥产品类别。现代聊天产品也可以带工具和 Agent 能力。
-->

---

# 课程路线

<div class="timeline-row">
  <div class="timeline-card"><div class="eyebrow">01 · 基本机制</div><h3>从大语言模型到 Agent</h3><p>生成、工具与执行循环</p></div>
  <div class="timeline-card"><div class="eyebrow">02 · 产品与用法</div><h3>如何交付一个任务</h3><p>任务说明、验收与环境</p></div>
  <div class="timeline-card"><div class="eyebrow">03 · 能力扩展</div><h3>信息与工具如何配合</h3><p>上下文、知识、记忆与分工</p></div>
  <div class="timeline-card"><div class="eyebrow">04 · 工程演进</div><h3>从回答到持续执行</h3><p>Prompt → Context → Harness</p></div>
</div>

<p class="note">理解这些机制，可以帮助我们判断任务如何开始、结果如何检查，以及卡在哪里。</p>

---
src: ./slides/01-llm-why-agent.md
---
---
src: ./slides/02-products-and-usage.md
---
---
src: ./slides/03-capability-stack.md
---
---
src: ./slides/04-engineering-evolution.md
---
