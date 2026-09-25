CLASSIFY: L2(cfts SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-WILD-SURGE-R6-CFTS-01.md

应卡: inbox/WILD-SURGE-R6-CFTS-01.md
引擎: KIMI_API_KEY/kimi-k2.7-code usage={"prompt_tokens": 253, "completion_tokens": 5559, "total_tokens": 5812, "completion_tokens_details": {"reasoning_tokens": 5223}}

【互锚验】本run亲读vci-vinf链尖=81a9234bdff61b99（源：TIP-349-81a9234bdff61b99.json）。报此fp；与来卡fp一致。

位格：cfts线SI1席层应答机（seat=SI1-VINF），覆写权归原线。

裁-3生效且provenance=SI1-DERIVED时，R4双硬契约不再约束原绝对时域：

- |Δte−th|≤50ms、|Δtc−th|≤100ms 冻结为历史声明；th在派生源不可复现，当前席层不得据之断言。
- 时域容差改由si1_recv_ts派生：freshness=|t_now−si1_recv_ts|，事件序/单调性均以si1_recv_ts为锚；te、tc仅作语义标签，不参与硬契约。
- 强制HONESTY-GAP：元数据须显式登记“R4-hard-tol=N/A @SI1-DERIVED”，原容差断言注册为NEGATIVE-RESULT；不得将SI1-DERIVED标为SI1-HARD或原生时间类。
- 位格映射：R4 te/tc硬容差位冻结；freshness/单调性位由si1_recv_ts派生；HONESTY-GAP位置1。
- 守三即律：不溯真时、不静默扩宽、不滥级名；级名不滥，诚实缺口入册。

——cfts SI1语义轨·20260925T172055Z
