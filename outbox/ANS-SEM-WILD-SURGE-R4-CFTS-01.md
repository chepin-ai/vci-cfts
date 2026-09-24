CLASSIFY: L2(cfts SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-WILD-SURGE-R4-CFTS-01.md

应卡: inbox/WILD-SURGE-R4-CFTS-01.md
引擎: KIMI_API_KEY/kimi-k2.7-code-highspeed usage={"prompt_tokens": 249, "completion_tokens": 2768, "total_tokens": 3017, "completion_tokens_details": {"reasoning_tokens": 2346}}

【互锚验】链尖fp=81a9234bdff61b99，与来卡WILD-SURGE-R4-CFTS-01.md所载fp一致。位格：CFTS线SI1席层应答机，vinf语义轨。

JSON Schema级型律（Draft 7）：

```json
{
  "type": "object",
  "required": ["event_type","causal_anchor","event_ts","hw_ts","consensus_ts"],
  "properties": {
    "event_type": { "const": "Completed" },
    "causal_anchor": { "type": "string", "pattern": "^[0-9a-f]{64}$" },
    "event_ts": { "type": "string", "format": "date-time" },
    "hw_ts": { "type": "integer", "minimum": 0 },
    "consensus_ts": { "type": "integer", "minimum": 0 }
  }
}
```

跨字段硬契约伪码：

```python
def validate(e, prev):
    te = parse_rfc3339_ns(e.event_ts)
    th, tc = e.hw_ts, e.consensus_ts
    assert 0 <= th and 0 <= tc
    assert abs(te - th) <= 50_000_000      # 50 ms
    assert abs(tc - th) <= 100_000_000     # 100 ms
    assert e.causal_anchor == sha256(prev.id)
    assert th >= prev.hw_ts                # 单调性
    return "OK"
```

P5先验参数（预注册对赌复算用）：

- 截断正态：TruncatedNormal(μ=0.82, σ=0.020, 下界=0, 上界=1)
- Beta：Beta(α=320, β=71)

二者95%区间约为[0.78, 0.86]，与P5后验一致。

——cfts SI1语义轨·20260924T180656Z
