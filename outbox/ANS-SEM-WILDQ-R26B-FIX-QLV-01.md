CLASSIFY: L2(qlv SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-WILDQ-R26B-FIX-QLV-01.md

应卡: inbox/WILDQ-R26B-FIX-QLV-01.md
引擎: DEEPSEEK_API_KEY/deepseek-chat usage={"prompt_tokens": 134, "completion_tokens": 1180, "total_tokens": 1314, "prompt_tokens_details": {"cached_tokens": 0}, "prompt_cache_hit_tokens": 0, "prompt_cache_miss_tokens": 134}

# 质量验证线审查意见

## (1) 对"可编译性"主张的充分性

**不充分。** 拆开看：

- **热跑 (cache命中, 17s)**：只验证"缓存可复用 + 链接可完成"。它证明的是 *artifact consistency*,不是 *source → binary* 的可重放性。任何 source 层面的破坏（宏、条件编译、路径依赖）都可能被缓存遮蔽。
- **冷跑 (清.lake重建, ~49min)**：这才是真正的可编译性证据。但它是**单一条件**下的可编译性——同一 toolchain、同一环境变量、同一平台。

**结论**：双证据覆盖了"缓存可复用性"和"从零可编译性"两个正交维度，但**未覆盖**：
- toolchain 版本漂移（仅测了当前锁定版本）
- 干净环境（无残留 env、无 user-level cache）
- 增量构建路径（`lake build` 单文件 vs 全量）
- 并行度变化下的确定性

若"可编译性"主张仅限 *"当前锁定环境下从零可编译"*，则**基本充分**（冷跑为主证据、热跑为回归护栏）。若主张是 *"任何合规环境可编译"*，则**不充分**，需补最小环境矩阵。

## (2) 跨rev矩阵：全跑 vs 抽样

**必须全跑，不能抽样。** 理由：

- 三个 rev 是**离散历史断面**（2f3d8f63 / 815bbf13 / 9fe29c4b），不是同一分布的连续样本——抽样无统计意义，只会漏掉 rev-specific 断裂。
- 冷跑 ~49min × 3 = ~2.5h，成本可控，**抽样省下的时间远低于漏检一个 rev 的代价**。
- `9fe29c4b` 标记为 `pin`：pin 本身是强约束点，必须完整验证；`815bbf13` 的 `CACHE_OK` 需要冷跑交叉确认，否则 `CACHE_OK` 可能是 stale cache 的假阳性。
- 若确实要压缩：优先**冷跑全跑**，热跑可只对新引入 rev 跑（热跑本就是回归护栏，历史 rev 的热跑收益递减）。

**建议**：3 rev × (冷跑必跑 + 热跑仅 rev 首次引入时跑)。

## (3) 验证报告必填字段集

```
# 身份
rev_hash                    # 完整 commit hash
rev_label                   # 如 2f3d8f63
run_mode                    # hot | cold
run_id                      # 唯一标识,可回溯
timestamp_start / end
operator                    # 人或CI job id

# 环境
toolchain_version           # lean/编译器精确版本
platform / arch
env_hash                    # 关键 env vars 的哈希
lake_manifest_hash
cache_state                 # cold=已清 | hot=命中率

# 结果
build_exit_code
build_duration_s
warnings_count / warnings_digest
errors                        # 非空则失败
artifact_hash                 # 产出二进制/object 哈希
cache_key                     # 热跑关键字段

# 交叉
cold_run_paired_run_id        # 热跑指向配对的冷跑
matrix_position               # {rev, mode} 在矩阵中的坐标
verdict                       # PASS | FAIL | BLOCKED
```

**最小强制集**：`rev_hash, run_mode, toolchain_version, env_hash, build_exit_code, artifact_hash, verdict, paired_run_id`。缺 `artifact_hash` 或 `env_hash` 则报告不可复现，视为无效。

## (4) 第三独立验证

**做，且必须做。** 委托方的冷热双跑是**同一执行者、同一方法**下的证据，二者共享系统误差：

- 若冷跑脚本本身漏清某个 cache 目录，热/冷都会"通过"。
- 若 toolchain 被静默 patch，两跑共享同一污染。

**第三独立验证的最小形态**：
1. **不同执行体**：不同机器 / 不同 CI runner / 不同用户环境。
2. **不同方法**：不调用委托方的 `lake` 封装脚本，直接用底层 toolchain 调 `lake build`；或对比 `artifact_hash` 与委托方声明的哈希是否一致。
3. **只跑 1 个 rev 的最小子集**即可（如 pin `9fe29c4b` 的冷跑），目的是**证伪**而非穷举。

**判定规则**：
- 第三验证 `artifact_hash` 与委托方冷跑一致 → 双跑证据可信。
- 不一致 → 双跑协议作废，先定位是脚本/环境/工具链哪层污染。

**成本**：1 rev 冷跑 ~49min + 环境准备，相对 2.5h 主矩阵是合理保费。

---

**一句话总结**：协议骨架对，但 (1) 给"可编译性"的授权过宽，(2) 3 rev 必须全跑冷跑，(3) 报告必须带 `artifact_hash`+`env_hash` 才可复现，(4) 第三验证不是可选项——它是把"双证据"从"自证"升级为"他证"的唯一手段。

——qlv SI1语义轨·20260930T014258Z
