---
theme: default
title: AI Agent 课程讲义
info: 面向非技术同事的 AI Agent 讲解课
class: hero-slide
mdc: true
drawings:
  persist: false
---

<div style="max-width: 78rem; margin: 0 auto;">
  <div class="eyebrow">AI Agent Course Notes</div>
  <div class="divider-line"></div>
  <h1 class="hero-title">AI Agent 到底是什么，为什么它变得这么有用</h1>
  <p class="lead">
    这不是一份“热点词扫盲”，而是要回答一个更实际的问题：
    为什么今天的 agent，已经不只是聊天机器人，而像会自主干活的员工？
  </p>

  <div class="frame" style="margin-top: 1.2rem; max-width: 62rem;">
    <div class="eyebrow">这节课要建立的理解：</div>
    <p class="mini-headline">Agent 不只是“更聪明的 LLM”，而是一套把模型、工具、状态和执行环境组织起来的软件系统。</p>
  </div>
</div>

---

# 如果把同一个任务交给 3 种系统，会发生什么

<div class="split-3">
  <div class="compare-card">
    <div class="eyebrow">传统 chatbot</div>
    <h3>“告诉你怎么做”</h3>
    <p>它会解释思路、给步骤、写答案，但通常停在“建议”。</p>
  </div>
  <div class="compare-card accent-panel">
    <div class="eyebrow">agent</div>
    <h3>“直接开始做”</h3>
    <p>它会读代码、跑命令、改文件、看结果、继续下一步。</p>
  </div>
  <div class="compare-card">
    <div class="eyebrow">workflow 系统</div>
    <h3>“按预设流程做”</h3>
    <p>它适合重复流程，但对临场判断和开放任务没那么灵活。</p>
  </div>
</div>

<div class="overlay-note">
  <strong>目标：</strong>
  解释清楚为什么 agent 比最早的 chatbot 强这么多，以及它的能力边界究竟来自哪里。
</div>

---

# 今天这节课，沿着 4 个阶段往前走

<div class="timeline-row">
  <div class="timeline-card">
    <div class="eyebrow">阶段 1</div>
    <h3>先理解 LLM</h3>
    <p>它到底怎么工作，为什么“词语接龙”已经足够强。</p>
  </div>
  <div class="timeline-card">
    <div class="eyebrow">阶段 2</div>
    <h3>再看为什么不够</h3>
    <p>为什么只会生成文本，还不足以完成真实任务。</p>
  </div>
  <div class="timeline-card">
    <div class="eyebrow">阶段 3</div>
    <h3>再看 agent 补了什么</h3>
    <p>运行时、工具、状态、环境交互、执行闭环分别解决什么问题。</p>
  </div>
  <div class="timeline-card">
    <div class="eyebrow">阶段 4</div>
    <h3>最后落到产品与用法</h3>
    <p>Claude Code / Codex 强在哪、边界在哪、怎么快速上手。</p>
  </div>
</div>


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
