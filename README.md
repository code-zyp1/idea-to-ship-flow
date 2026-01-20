- # idea-to-ship-flow

  一套通用的提示词工作流，把“很粗/很乱的想法”快速推进到：
  - 可执行的 Spec Brief
  - 可直接提交到仓库的 PRD/Plan/Decisions/Checklist
  - 两段可复制的实现/审计启动提示词（Claude Code / Codex/GPT）
  
  特点：
  - 默认倾向 v1 一次到位（不强推多版本迭代）
  - 但必须有：范围锁定 + 降级策略
  - 强调工程化验收（可测试、可判定、尽量脚本化）
  - 文档产物可落库，不依赖对话上下文

  ---
  
  ## 文件

  - `想法孵化-1.md`：用最少轮次把想法变成“可进入 Spec Brief”
  - `澄清规格-2.md`：把乱需求收敛为可执行 Spec Brief（固定 13 条结构）
  - `工程文档生成器-3.md`：从 Spec Brief 生成 4 份仓库文档 + 2 段启动提示词

  ---
  
  ## 推荐使用方式
  
  ### 1) 想法孵化（Stage 1）
  把一句话想法/截图描述/链接丢给 `想法孵化-1.md`。
  
  输出会很短：目标 + 3 个关键问题（A/B 默认）+ 最小信息清单。
  
  当信息足够时，会出现：
  ✅ 已可进入：澄清规格（Spec Brief）

  **注意：这个 ✅ 只表示“够进入 Spec Brief”，不表示信息完备。**
  
  为避免你“没注意继续聊很多轮”，Stage 1 在 ✅ 后会强制你二选一：
  - `LOCK`：锁定默认假设，立刻进入 Spec Brief（推荐）
  - `EXPLORE`：允许再补一轮（最多 3 个问题），然后强制进入 Spec Brief
  
  ---
  
  ### 2) 澄清规格（Stage 2）
  把 Stage 1 的结论 + 你的补充丢给 `澄清规格-2.md`，生成 Spec Brief。
  
  Spec Brief 末尾会提示：
  ✅ 已可进入：工程文档生成器（Doc Generator）
  
  并要求你二选一：
  - `LOCK`：锁定 Spec Brief
  - `REVISE`：补充信息并生成 v0.2（最多追问 5 个问题）
  
  ---

  ### 3) 工程文档生成（Stage 3）
  把已 LOCK 的 Spec Brief 丢给 `工程文档生成器-3.md`。
  
  它会输出：
  - docs/prd.md
  - docs/plan.md
  - docs/decisions.md
  - docs/checklist.md
  - Claude Code 实现启动提示词
  - Codex/GPT 审计启动提示词
  
  ---
  
  ## 常见问题
  
  ### Q: 为什么 Stage 1 第一轮就 ✅ 已可进入，但后面补充后更全面？
  A: 因为 Stage 1 的目标是“够进入 Spec Brief”，不是“把细节补全”。补全细节应该在 Stage 2 做。  
  所以 Stage 1 在 ✅ 后会强制你 LOCK/EXPLORE，避免无限对话。
  
  ### Q: 我在 ✅ 之后继续自然对话会怎样？
  A: 模板要求 AI 提醒你用 LOCK/EXPLORE/REVISE，不要无限追加新问题。

  ---

  ## License
  MIT