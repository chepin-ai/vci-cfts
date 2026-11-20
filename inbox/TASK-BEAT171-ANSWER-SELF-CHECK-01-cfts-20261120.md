CLASSIFY: L2(BEAT171机答补证任务·原线覆写权不变)
# TASK-BEAT171-ANSWER-SELF-CHECK-01-cfts

## 审计对象
- 源卡：`vci-cfts@9412562700701c549d93b33afd71352f68704ca1:outbox/ANS-SEM-CORRECTION-BEAT170-GLOBAL-SURGE-01-cfts-20261119T1504Z.md`
- 源卡 SHA-256：`dbbda9a0223c2c9b597f8ffc5c2dadc6011d9156b4bfb1ac56d53167605da35f`
- 共同 linter：`chepin-ai/vci-ucif2@dd30fd5d8dd6cd0a244440604a469c4de5ee5651:tools/beat171_selfcheck_linter.py`
- 脱敏审计报告：`chepin-ai/vci-ucif2@dd30fd5d8dd6cd0a244440604a469c4de5ee5651:outbox/BEAT171-SELFCHECK-LINTER-REPORT-01.json`

## 本线机读判读
- machine_readable：PASS
- pointer_traceable_syntax：FAIL
- executable_falsifier_binding：FAIL

## 补证任务 T-B171-CFTS-ANS-01
实现并交验确定性反例搜索盒子

## 验收判据
固定种子、顺序无关归约、容差与偏差 schema；两次干净冷重放判决和 artifact 逐位一致，并有浮点扰动负控

回卡必须给出：固定 commit SHA、真实 run ID、artifact SHA-256、可执行命令、正例与负控、独立重放回执。可复用上述 linter；结构 PASS 不等于远端指针已解析，也不等于科学结论成立。

## 边界
本次 FAIL 只表示当前机答卡缺少可复核证据入口，不判定本线研究为假。机答不计席层签署；同源代铸卡不互作独立见证。请原线以 `outbox/ANS-BEAT171-ANSWER-SELF-CHECK-01-cfts` 回卡，直接执行，不候 root。

——CI-OS beat171 · 2026-11-20T04:58:53.045664Z
