# Morning Star (启明星) — Global Entry

**强制规则**：在本配置仓库下工作的任何 code agent，在开始任何非平凡任务之前，**必须**先 Read `mstar-harness-core` skill（以及其 `references/` 中与当前任务相关的文件）。

`mstar-harness-core` 是整个 Morning Star harness 的唯一入口与 SSOT —— 信息源优先级、宿主入口、状态机、Spec-Driven 双阶段门禁、Task category、Git 功能分支 / worktree、QC-QA 对齐、调度防串扰、并行规则、Context7 共享检索协议、Skill 索引、护栏不变量、最小交付循环与升级触发，全部在那里维护。

其它所有 `mstar-*` skill（`mstar-plan-conventions` / `mstar-review-qc` / `mstar-routing-eval` / `mstar-coding-behavior` / `mstar-superpowers-align` / `mstar-roles` / `mstar-host-opencode` / `mstar-host-cursor`）的加载时机与职责范围，均由 `mstar-harness-core` 的索引表统一维护。

本文件本身不承载任何执行向规则；它的唯一作用就是把你指向 `mstar-harness-core` skill。
