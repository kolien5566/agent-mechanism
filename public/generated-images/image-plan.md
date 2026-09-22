# 课程配图资产索引

当前 Slidev 使用以下 **14 张原版图片**，位于 `public/generated-images/`，页面通过 `/generated-images/<文件名>` 引用。此次恢复原图保留 **62 页**及已修改的文字、讲者备注和课程结构。

对应的 `*-v2.png` 文件保留供追溯，当前课件不引用。原版图片保持原有构图、标签和视觉表现。

## 当前资产

| 文件 | 章节 | 主题 |
|---|---|---|
| `llm-next-token.png` | Part 1 | LLM 的下一个 token 预测与连续生成。 |
| `from-chat-to-agent.png` | Part 1 | 从聊天问答到 Agent 执行任务。 |
| `llm-inside-agent-system.png` | Part 1 | 模型在 Agent 系统中的位置。 |
| `agent-loop.png` | Part 1 | Agent 的判断、行动与反馈循环。 |
| `human-in-the-loop.png` | Part 1 | 人工参与 Agent 执行过程。 |
| `shell-access-boundary.png` | Part 1 | Shell 与 Agent 的执行能力。 |
| `agent-product-core.png` | Part 2 | Agent 产品入口与工作机制。 |
| `codex-task-to-result.png` | Part 2 | Codex 从任务到结果的工作流程。 |
| `agent-capability-stack.png` | Part 3 | Agent 能力组成总览。 |
| `mcp-primitives.png` | Part 3 | MCP 的 Tools、Resources 与 Prompts。 |
| `skill-pack.png` | Part 3 | Skill 任务资料包。 |
| `subagents-task-split.png` | Part 3 | 子 Agent 的任务分工与汇总。 |
| `harness-system-loop.png` | Part 4 | Harness 与 Agent 执行系统。 |
| `prompt-context-harness.png` | Part 4 | Prompt、Context 与 Harness 的工程演进。 |

## 使用与维护

- 图片来源使用项目内路径；原图与 v2 文件分别保存，避免覆盖。
- 配图切换不增删页面。变更后核对 62 页、图片加载和完整展示情况。
- 后续如调整图片版本，同步更新本索引和章节 Markdown 中的引用。
