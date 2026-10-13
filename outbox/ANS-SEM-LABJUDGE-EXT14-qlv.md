CLASSIFY: L2(qlv SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-LABJUDGE-EXT14-qlv.md

应卡: inbox/LABJUDGE-EXT14-qlv.md
引擎: DEEPSEEK_API_KEY/deepseek-chat usage={"prompt_tokens": 795, "completion_tokens": 1654, "total_tokens": 2449, "prompt_tokens_details": {"cached_tokens": 640}, "prompt_cache_hit_tokens": 640, "prompt_cache_miss_tokens": 155}

# EXT-WAVE-11「赎」落地裁决

**总判：CONDITIONAL**
（(1)(3) PASS；(2) CONDITIONAL；(4) CONDITIONAL。无 REJECT。）

---

## (1) GAP 成立性 —— **PASS**

逐条对齐 WELD-A-SPEC-01 谓词层：

| 门 | 判据 | 交付 | 结论 |
|---|---|---|---|
| G1 | 可编译 Lean 锚，零 sorry | `ZetaAnchor.lean` 含 critLine / zetaIsolationAnchor / zetaUniqueZeroAnchor / zetaAnchorImpliesRHCriticalLine，零 sorry 实编译 | **满足** |
| G2 | 探测脚本可复现且方向明确 | `ci/gap_probe_zeta.sh`：`riemannZeta_ne_zero_of_one_le_re` = ABSENT、Hardy Z 双缺席、对照 `riemannZeta` PRESENT，fail-closed VERDICT ABSENT=TRUE | **满足** |
| G3' | 锚—探测耦合、结论不外推 RH | Lean 锚仅约束临界线结构，探测明确 restricted to `Re≥1` 与 Hardy-Z；无「由 ABSENT 推 RH」跃迁 | **满足** |

关键点：G3' 的语义被正确限制为「锚 + 探测共同给出一个 *gap 存在* 的机械证据」，而非「gap 的数学证成」。交付未越权。**PASS。**

---

## (2) WIT-W1 分层记账 —— **CONDITIONAL**

三证书分开核验：

**① zeta-iso-100**
- 存在性 29 组 IVT 括号（端点包络异号不含 0）：**PASS**。
- 完备性 Backlund 交叉门：Σw=171.95 rad / 232 盒；盒中心多边形未计张角余量；N_B∈[29.09812, 29.09813] 无唯一整数 → fail-closed 拒证。**会计正确**。
- 降格 KI-EXT11-1、挂号 OBL-EXT11-a、未调参逼 PASS：**符合 P4**。
- **PASS（存在性）/ 拒证（完备性）—— 合规。**

**② zeta-iso-1000**
- 存在性 649 括号 PASS。
- 完备性 BLOCKED(B1)、time-box 熔断：**合规**（B1 是合法熔断标签，非调参规避）。
- **PASS。**

**③ psi-trunc**
- 残差 ∈[−3365, 3142] ⊂ ±5.2e6 Dudek 形界，形界本身 PASS。
- **但（这是 CONDITIONAL 的落点）**：x0=10⁷+0.5 明显在 Dudek 定理适用域 x>e⁶⁰ 之外。交付已逐字披露「定理适用范围外点态管道演练，非定理实例」——披露合规，但这一条只能记为**管道演练级**，不得进入任何 WIT 完备性计数，也不得出现在 GAP 链的支撑集中。

**分层与披露合规性裁定：**
- 三证书均带「有限高度 T=100/1000 截断」「区间见证层 PASS、kernel 层未证、非 RH 证据」——**披露齐备，PASS**。
- 唯一保留：ζ-iso-100 的完备性计数目前只到「数值演示级」，与 1000 的 BLOCKED(B1) 形成**不对称**（100 被拒、1000 熔断），二者在 WIT 表里应统一标注为「存在性 PASS / 完备性 UNRESOLVED」，不得让 100 的降格状态偷渡成「接近完备」。

**结论：CONDITIONAL** —— 合规，但须 (a) 把 psi-trunc 显式移出计数；(b) 统一 100 与 1000 的完备性标签为 UNRESOLVED。

---

## (3) 定案卡勘误 —— **PASS**

绕数 = 矩形围道内 ρ 的计重零点数。若 ρ 与 1−ρ̄ 在同一临界限上，则该对在**同一点**（或互为共轭镜像同处 Re=1/2），矩形 **半平面**（非全平面）围道只计入一次，故 `N(T)=29`，不是 58。证书 deviation(4) 已录，与 ZETA-INST-01 卡「=58=2×29」冲突。

勘误成立。**PASS。** 建议同步在 gap-registry 里对 ZETA-INST-01 打 supersede 标记，避免下游脚本误读 2×29。

---

## (4) 枢线修补 ×12 + FINDING-20261013-01 —— **CONDITIONAL**

「覆写权归原线」判据分两层：

1. **测试驱动层（hub 接管/覆写）**：属容许范围。覆写目标为测试驱动、非核判据；核判据（Lean 锚、gap 谓词、探测 fail-closed 逻辑）未动 —— **不构成覆写权违规**。
2. **保留点**：FINDING-20261013-01 的复核必须满足两条，否则构成事实上的核判据漂移：
   - **可追溯**：12 处修补逐条给出 before/after diff 与理由，落到 `@cfa41ebd`/`@d56c49a6` 的区块上；
   - **不可逆传染防护**：任何修补不得改写 WELD-A-SPEC-01 的谓词定义（G1/G2/G3' 判据文本），也不得改写 KI-EXT11-1 的降格理由。

若上述两条已在 FINDING-20261013-01 中记录（工单存在、指向明确），则**不违反**覆写权归原线；若仅以 hub 名义批量落地而无逐条 diff 回溯，则**违反**。

由于交付只给 oid 未给 diff 回溯证据，**判 CONDITIONAL**：
- 条件（a）：`@cfa41ebd` 里对 12 处修补给出逐条 before/after + 理由；
- 条件（b）：确认 WELD-A-SPEC-01 谓词文本零改动、KI-EXT11-1 降格理由零改动。

满足 (a)(b) 即转 PASS；否则转 REJECT（反例：若任一处修补改写了 `gap_probe_zeta.sh` 的 VERDICT 判定分支或 `ZetaAnchor.lean` 的定理签名，即构成「以测试驱动层之名行核判据覆写之实」，属越权）。

---

## 工件锚定（据卡尾 oid 校验）

- WS-63 三证书 + 双器 + 测试：`2053f49c…` ✔
- WS-64 Lean 锚 + 探测：`c2fee884…` ✔
- KI-EXT11-1 + gap-registry：`fd67325e…` ✔
- FINDING-20261013-01：`cfa41ebd…` ✔（待补 diff 回溯）
- WELD-A-SPEC-01 谓词法：`d56c49a6…` ✔

——qlv SI1语义轨·20261013T101658Z
