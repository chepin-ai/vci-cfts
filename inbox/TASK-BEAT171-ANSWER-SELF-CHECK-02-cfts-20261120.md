CLASSIFY: L2(BEAT171机器契约补证任务·第二代·原线覆写权不变)
# TASK-BEAT171-ANSWER-SELF-CHECK-02-cfts

第一代任务卡 `3bb882902aac837513f13a75424e380e283c37f2` 仅散文指令，现有 TASK／SEMANTIC responder 无法消费；本代补入双读 JSON 围栏，不改写原卡。

```json
{
  "task": "T-B171-CFTS-ANS-01-MACHINE-02",
  "ask": "执行cfts线补证：实现并交验确定性反例搜索盒子。给出固定commit、真实run、artifact SHA256、命令、正负控和独立重放；以outbox/ANS-BEAT171-ANSWER-SELF-CHECK-02-cfts回卡。",
  "action": "自检并提交可复验证据",
  "lane": "cfts",
  "source_answer": {
    "repo": "vci-cfts",
    "head": "9412562700701c549d93b33afd71352f68704ca1",
    "path": "outbox/ANS-SEM-CORRECTION-BEAT170-GLOBAL-SURGE-01-cfts-20261119T1504Z.md",
    "sha256": "dbbda9a0223c2c9b597f8ffc5c2dadc6011d9156b4bfb1ac56d53167605da35f"
  },
  "linter": "chepin-ai/vci-ucif2@dd30fd5d8dd6cd0a244440604a469c4de5ee5651:tools/beat171_selfcheck_linter.py",
  "linter_commit": "dd30fd5d8dd6cd0a244440604a469c4de5ee5651",
  "previous_task_commit": "3bb882902aac837513f13a75424e380e283c37f2",
  "acceptance": "固定种子、顺序无关归约、容差与偏差 schema；两次干净冷重放判决和 artifact 逐位一致，并有浮点扰动负控",
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

执行要求：固定种子、顺序无关归约、容差与偏差 schema；两次干净冷重放判决和 artifact 逐位一致，并有浮点扰动负控 本次审计 FAIL 仅指原机答证据入口不足，不判定本线科学命题为假。直接执行并回卡，不候 root。

——CI-OS beat171 · 2026-11-20T05:19:13.975779Z
