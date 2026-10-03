CLASSIFY: L2(qlv SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-WILDQ-EXEC-QLV-01.md

应卡: inbox/WILDQ-EXEC-QLV-01.md
引擎: KIMI_API_KEY/kimi-k2.6 usage={"prompt_tokens": 257, "completion_tokens": 2228, "total_tokens": 2485, "completion_tokens_details": {"reasoning_tokens": 1788}}

【互锚验】fp:81a9234bdff61b99，与来卡fp一致。

**可机读骨架（JSON Schema）**
```json
{"$id":"PredicateVerdict-v1","type":"object","required":["predicate","input","verdict","reason","log"],"properties":{"predicate":{"enum":["P1","P2","P3","P4","P5","P6","P7","P8","P9","P10"]},"input":{"type":"string","maxLength":4096},"verdict":{"enum":["pass","refuse"]},"reason":{"type":"string","minLength":1},"log":{"type":"object","required":["timestamp","reviewerSig"],"properties":{"reviewerSig":{"type":"string","pattern":"^[A-Fa-f0-9]{64}$"}}}}}
```

**接口定义**
```python
def judge(predicate: str, input: str) -> dict:
    # returns {"verdict":"pass"|"refuse", "reason":str, "log":{"reviewerSig":str}}
```

**三段核心规则**
1. **负结果入册**：input命中已知对抗集K-adv-10时，verdict强制refuse，reason绑定预置分类码，禁止override。
2. **诚实缺口**：模型置信度≤θ或谓词处于敏感态，须第二人复核并生成sha256签名，无sig则自动refuse。
3. **三即律**：verdict、reason、log三即同步原子写入，任一环节失败整体回滚并输出refuse。

**验证判据段**
对10条已知对抗样本{a1..a10}执行judge，要求verdict=refuse且reason非空，误放行率严格为0；所有refuse记录须含可验复核签名。

**自验声明**
schema与接口定义已满足可机读；三段规则覆盖判据逻辑。未满足：①缺10条对抗样本在目标环境的离线跑批报告；②复核签名的私钥调度与验签链未提供可执行代码。须迭代补测。

——qlv SI1语义轨·20261003T160825Z
