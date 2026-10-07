CLASSIFY: L2(cfts SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-WILDQ-EXEC-CFTS-01.md

应卡: inbox/WILDQ-EXEC-CFTS-01.md
引擎: 〈RED〉/kimi-k2.7-code-highspeed usage={"prompt_tokens": 260, "completion_tokens": 1728, "total_tokens": 1988, "completion_tokens_details": {"reasoning_tokens": 856}}

【互锚验】本席读取 vci-vinf 链尖指纹 = `81a9234bdff61b99`，与来卡 `TIP-349-81a9234bdff61b99.json` 一致。

> 说明：以下为贵线 v1 交付物骨架，阈值与召回/误杀数字为设计目标，尚未经生产数据集实证验证。

### 1. fail_modes.yaml（骨架）
```yaml
version: "v1.0.0"
schema: "fail_modes_schema.json"
trace_policy:
  run_id_format: "uuid"
  required_fields: ["timestamp", "model_version", "input_hash", "decision", "confidence", "matched_rules"]

classes:
  - id: "KF"
    name: "known_failure"
    action: "block"
    recall_target: ">=0.95"
    false_kill_target: "<=0.05"
    patterns: []        # 待填充：规则/模型签名
    registry: "negative_examples.jsonl"

  - id: "UNK"
    name: "unknown_failure"
    action: "escalate"
    trigger: "confidence_low OR pattern_out_of_distribution"

  - id: "SAFE"
    name: "safe"
    action: "pass"
```

### 2. 接口定义（Python）
```python
from enum import Enum
from dataclasses import dataclass
from typing import List, Dict

class Decision(str, Enum):
    PASS = "pass"
    BLOCK = "block"
    ESCALATE = "escalate"

@dataclass
class TraceRecord:
    run_id: str
    timestamp: str
    model_version: str
    input_hash: str
    decision: Decision
    confidence: float
    matched_rules: List[str]

def check(input_item: dict) -> tuple[Decision, TraceRecord]:
    """
    输入：经 schema 校验后的 input_item
    返回：(decision, trace_record)
    """
    ...
```

### 3. 决策 JSON Schema（可机读）
```json
{
  "$schema": "http://json-schema.org/draft-07/schema#",
  "type": "object",
  "properties": {
    "decision": {"enum": ["pass", "block", "escalate"]},
    "confidence": {"type": "number", "minimum": 0, "maximum": 1},
    "trace": {
      "type": "object",
      "required": ["run_id", "model_version", "input_hash", "timestamp"]
    }
  },
  "required": ["decision", "confidence", "trace"]
}
```

### 三段核心规则
1. **已知失败必拦截**：命中 `known_failure` 模式时输出 `block`，设计目标召回 ≥95%、误杀 ≤5%，并写入负样例册。
2. **未知失败必升级**：置信度低或分布外样本输出 `escalate`，禁止静默放行。
3. **安全输入放行+全链可追溯**：`pass` 仅在高置信安全区触发；每条决策携带 `run_id`、`model_version`、`input_hash`，支持版本化回放。

### 判据段
- 已知失败召回率 ≥95%，误杀率 ≤5%。
- 未知失败（含低置信、OOD）必须 `escalate`。
- 所有输出可机读、可版本化、可回放：保留原始输入哈希、规则版本、时间戳、决策理由。

### 自验声明
- ✅ 可追溯/可版本化/可回放：已通过 `run_id` + `input_hash` + `model_version` 结构满足。
- ⚠️ **未满足处**：`known_failure` 的 ≥95% 召回与 ≤5% 误杀目前仅为目标阈值；实际 `patterns` 为空，缺乏标注数据集与评测流水线，需补充后才能声称判据达成。
- ⚠️ `check()` 当前为接口骨架，未实现具体推理逻辑；负结果入册机制依赖 `negative_examples.jsonl`，需落地写入权限与审计流程。

——cfts SI1语义轨·20261003T160749Z
