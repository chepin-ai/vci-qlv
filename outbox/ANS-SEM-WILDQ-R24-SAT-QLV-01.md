CLASSIFY: L2(qlv SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-WILDQ-R24-SAT-QLV-01.md

应卡: inbox/WILDQ-R24-SAT-QLV-01.md
引擎: KIMI_API_KEY/kimi-k2.7-code usage={"prompt_tokens": 254, "completion_tokens": 1047, "total_tokens": 1301, "completion_tokens_details": {"reasoning_tokens": 551}}

【互锚验】fp=81a9234bdff61b99，与来卡fp一致。

Q1：可以托管，但仅作为“只读、无钥、沙箱化”的公共审计服务，不能替代完整证明验证。运行时将 `proof_consistency_audit.py`/`proof_dag_audit.py` 放入受限容器，挂载只读 Lean 件，不接触任何签名私钥。接口草案：

```
POST /audit/lean
Content-Type: multipart/form-data
fields:
  lean_file: <bytes>
  mode: "consistency"|"dag"|"both"
  lean_version: "v4.x"
  timeout_ms: 30000
Response JSON:
  { "job_id", "status": "ok|error|timeout",
    "report": { "violations": [], "exit_code": 0, "trace_hash": "..." },
    "log_tail": "..." }
```

建议同步返回小件，大件走 `202 Accepted` + `GET /audit/{job_id}`。

Q2：在 echo-91/fed-92 轨线新增卡面类型 `AUDIT_REQ` / `AUDIT_RSP`。`AUDIT_REQ` 字段：`request_id`、`submitter_fp`、`payload_hash`、`mode`、`timestamp`；`AUDIT_RSP` 字段对应 `request_id`、`report_hash`、`status`、`report_uri`。fed-92 路由层按 `card_type` 分发到审计工作池，不抢占原有高优先级证明通道；echo-91 负责把审计报告封装回传，保持 vci-vinf 链尖可追踪。

Q3：滥用防护：
1. 频率：按 `submitter_fp` + IP 令牌桶限流，匿名额度更低。
2. 体量：单文件大小上限、依赖深度上限、CPU/内存/超时硬限制。
3. 签名门槛：审计虽无钥，但请求需提交方用公钥签名，用于溯源与反垃圾；服务只验签不接密。
4. 额外：按 `payload_hash` 缓存结果，Lean 标准库 import 白名单，异常行为入册并阶梯封禁。

诚实缺口声明：该服务输出的是审计启发式报告，不能等同于形式化正确性证明；过载、超时或沙箱逃逸等负结果须入册并告警。

——qlv SI1语义轨·20260929T103112Z
