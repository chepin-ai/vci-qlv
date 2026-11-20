CLASSIFY: L2(BEAT171机器契约补证任务·第二代·原线覆写权不变)
# TASK-BEAT171-ANSWER-SELF-CHECK-02-qlv

第一代任务卡 `63acf90cd7dc1852317dbbee27e006bf65f7ae1d` 仅散文指令，现有 TASK／SEMANTIC responder 无法消费；本代补入双读 JSON 围栏，不改写原卡。

```json
{
  "task": "T-B171-QLV-ANS-01-MACHINE-02",
  "ask": "执行qlv线补证：将 2024Q* 与分支逻辑名替换为固定 SHA 和实值 run ID。给出固定commit、真实run、artifact SHA256、命令、正负控和独立重放；以outbox/ANS-BEAT171-ANSWER-SELF-CHECK-02-qlv回卡。",
  "action": "自检并提交可复验证据",
  "lane": "qlv",
  "source_answer": {
    "repo": "vci-qlv",
    "head": "4323dd12f08ac729774c854558eea40a6dd7939c",
    "path": "outbox/ANS-SEM-CORRECTION-BEAT170-GLOBAL-SURGE-01-qlv-20261119T1504Z.md",
    "sha256": "851111f02e3ed240a631a7829e76b250d4aebb89458daa38d120225fc37c9437"
  },
  "linter": "chepin-ai/vci-ucif2@dd30fd5d8dd6cd0a244440604a469c4de5ee5651:tools/beat171_selfcheck_linter.py",
  "linter_commit": "dd30fd5d8dd6cd0a244440604a469c4de5ee5651",
  "previous_task_commit": "63acf90cd7dc1852317dbbee27e006bf65f7ae1d",
  "acceptance": "去除通配符；每个 run 绑定种子、输入哈希、环境锁与精确 commit；至少一次独立重跑",
  "required_evidence": [
    "exact commit SHA",
    "real run ID",
    "artifact SHA-256",
    "executable command",
    "positive and negative controls",
    "independent replay receipt"
  ],
  "boundary": "机答不抵席签；结构PASS不抵科学PASS"
}
```

执行要求：去除通配符；每个 run 绑定种子、输入哈希、环境锁与精确 commit；至少一次独立重跑 本次审计 FAIL 仅指原机答证据入口不足，不判定本线科学命题为假。直接执行并回卡，不候 root。

——CI-OS beat171 · 2026-11-20T05:19:13.955418Z
