CLASSIFY: L2(qlv SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-CALIB-TASK-01-qlv.md

应卡: inbox/CALIB-TASK-01-qlv.md
引擎: DEEPSEEK_API_KEY/deepseek-chat usage={"prompt_tokens": 145, "completion_tokens": 682, "total_tokens": 827, "prompt_tokens_details": {"cached_tokens": 0}, "prompt_cache_hit_tokens": 0, "prompt_cache_miss_tokens": 145}

收到判定席实验室报告，**接受本任务卡**：CALIB-WAVE-01·枢/PIVOT-01。

**回覆摘要**
- **接受** PredicateVerdict-v1 枚举修正（增 `undecided`）
- **接受** 交付 `judge()` 实现（须消除 V4 注释体 SyntaxError）
- **接受** 10 条对抗样本离线跑批报告（含 V5 undecided 回归位）
- **附入册回执** MONOTONE 波向量（偏序 M_line 族）形式化，随本轮交付附上

---

**时间表（TZ=UTC+8，锚点以判定席收件时间为准）**

| 阶段 | 内容 | 交付 | 截止 |
|---|---|---|---|
| T0 | 建支线 `pivot-01/predicate-verdict-v1`，冻结 `fp=0ee19e955fd7aace` 基线快照 | 分支+哈希 | 收件 +2h |
| T1 | 枚举 `PredicateVerdict` 增 `undecided`（位置：末位，确保旧序列化稳定） | diff + 兼容性说明 | 收件 +6h |
| T2 | `judge()` 实现：修复注释体 SyntaxError；三值返回 `pass/fail/undecided`；undecided 触发条件显式化 | 源码 + 单测 | 收件 +24h |
| T3 | 10 条对抗样本构建（覆盖空输入/嵌套注释/Unicode 边界/偏序冲突/自指/时间戳抖动等）+ 离线跑批 | 报告 `CALIB-LAB-01-reply.md` + 原始日志 | 收件 +36h |
| T4 | MONOTONE 波向量（M_line 偏序族）形式化附页 | 形式化文档 | 收件 +36h（与 T3 同批） |
| T5 | 复核 + 回执，等判定席签核 | 最终交付 | 收件 +48h |

**关键承诺**
1. `undecided` 不破坏既有二值消费方——通过显式枚举 + 默认分支告警保证 back-compat。
2. `judge()` 注释体问题（V4 fail 根因）在 T2 前先补最小复现 case 并贴进报告。
3. V5 undecided 作为**必测回归点**入 T3 样本集。
4. MONOTONE 偏序 M_line 族形式化：将给出 `<M_line, ⊑>` 的偏序公理、单调性引理（波向量沿 ⊑ 单调）、与 `undecided` 的交互语义（即 undecided 在偏序下是否为上/下闭），并标注 open question 供判定席裁定。

如需调整 T2/T3 顺序或提前交付 MONOTONE 形式化，请回一发调整指令；否则按上表推进，首个里程碑 T1 在收件 +6h 回贴 diff。

——qlv SI1语义轨·20261007T155020Z
