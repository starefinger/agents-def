# 宿主适配：Cursor（含 `/pm`）

本文件描述在 **Cursor** 中使用本仓库时的**入口、加载顺序与能力差异**。流程规则仍以根目录 `AGENTS.md` 与各专题文档为准；此处只补「Cursor 上怎么接」。

## 推荐入口

1. **全局规则与索引**：`~/.config/opencode/AGENTS.md`（与 OpenCode 共用同一份**中性** harness；Cursor 不会自动注入，需通过规则或手动 Read）。
2. **项目经理行为**：`~/.config/opencode/agents/project-manager.md`（用户可通过 `**/pm`** 等指令让主代理按 PM 角色执行时读取）。
3. **本文件**：明确 Cursor 与 OpenCode 的能力差，避免假设「一定能 `@` 起子代理」。

## 重要限制：通常没有“真·子代理”队列

在 Cursor 中，**主 Composer/Agent 会话**往往**不能**像 OpenCode 那样稳定地 `**@role` 唤起独立 subagent 会话**并行执行 Assignment。

因此 PM 编排需降级为以下**可执行模式**（择一或组合，并在 Status Update 中说明你用的是哪种）：

### 模式 A — 单会话多帽（默认）

同一对话中由**主代理**顺序执行：先以 PM 规划并写出 Assignment，再在同一会话用**显式声明**切换执行身份，例如：

- `Acting as role: fullstack-dev — executing Assignment …`
- 执行前 **Read** 对应 `~/.config/opencode/agents/<role>.md`，严格按该文件的产出与门禁执行，视同「被派工的专责代理」。

QC/QA 等多视角审查也可在同一会话内分轮次进行，每轮开始前 Read 对应 `agents/qc-specialist*.md` / `agents/qa-engineer.md`，并保持 `**plan_id` / `Review range` 与 OpenCode 流程逐字一致**（见 `harness-loop.md`、`plan-convention.md`）。

### 模式 B — 多窗口 / 多会话扮演

将每条 Assignment 放到**新聊天**，在首轮消息中粘贴 Assignment 并要求代理 Read 对应 `agents/<role>.md`。适合长实现，避免单会话上下文挤压；PM 在主线会话汇总证据与状态。

### 模式 C — 宿主并行能力（若可用）

若当前 Cursor 版本提供 **并行 Task / 多代理** 且行为与「独立上下文」等价，**且**满足 harness 对 **worktree**、**分支策略**的要求，可按 Assignment 分拆并行；否则不要因为「看起来像能并行」而绕过 `harness-loop.md` 里对同仓并发写入的约束。

## 澄清交互

- **无 `question` 工具时**：用结构化 Markdown（标题、选项列表）在正文中提问，或用 Cursor 支持的等价交互；原则与 `harness-loop.md` 的 `clarify` 一致。
- **不要把「能问」当成「已澄清」**：高影响歧义未收敛仍须 `Blocked` 或升级人工。

## Superpowers 与技能

无内置 Skill 工具时：按 `library-docs-and-hosts.md` 与 `superpowers-skills.md` 的 **「未安装插件时」**，用 **Read** 打开上游 `SKILL.md` 再执行步骤。

## 与项目规则的关系

自 cwd 向上的项目 `AGENTS.md` / `CLAUDE.md` 优先于全局 harness；与 `project-manager-mode` 等 Cursor 规则冲突时以项目规则与用户当轮指令为准。

## OpenCode 对照

OpenCode 下的加载与子代理语义见 `**host-opencode.md`**。