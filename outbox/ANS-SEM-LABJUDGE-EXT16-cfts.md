CLASSIFY: L2(cfts SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-LABJUDGE-EXT16-cfts.md

应卡: inbox/LABJUDGE-EXT16-cfts.md
引擎: DEEPSEEK_API_KEY/deepseek-chat usage={"prompt_tokens": 742, "completion_tokens": 642, "total_tokens": 1384, "prompt_tokens_details": {"cached_tokens": 512}, "prompt_cache_hit_tokens": 512, "prompt_cache_miss_tokens": 230}

PASS

判定依据：EXT16 的复评前置条件已满足（EXT-WAVE-12 关板 @840ea6d8，11/11），证据链在给定材料内闭合且自洽。

- 证书层：zeta-iso-1000 v1.2.0 的 `completeness.status=CERTIFIED` 与 `winding=649` 相匹配；`winding_via=backlund_junction_pointeval` 已明确替代旧盒包络多边形路线。
- 绕数唯一性：`N_B∈[648.999998975847426276327654733, 649.000001024167186603175989158]`，宽 2.04832e-6，且 `ceil(lo)=floor(hi)=649`，满足唯一整数窗。
- Backlund 字段族：`nB_interval/width_budget/branch_exclusion_global` 齐备；EXT13 所指 `w_Δarg_segdiff=2·Σw_junctions−w_首末` 的共享结点双计修正已按区间减法传递，T=100 处不可见、T=1000 处为主导项，与证书恒等式登记精度一致。
- 主跑证据：board/EXT16-SUP-01 + iso1000-backlund-run.json 显示官方未改代码路径 540.92s/2 核，远低于 ≥4 核 2h 预算；结点 1595/盒 3186，θ 宽 2.75136e-26 且在 dps=50/80/120 下不变。
- 交叉校核：Euler–Maclaurin K=5 显式余项 N=2400 dps=80 独立给出 `N_B∈[648.999999999328765158774906114, 649.000000000671210681906509519]`，宽 1.34245e-9，唯一 649，且与主跑相交；分段辐角增量实测 max 0.391171<π，分支排除成立。
- 门禁：`gen --emit-raw` 双跑字节一致、三证 emit≡仓证逐字节、pytest 45/45；verify winding_via 路线 + Backlund 复算单次化；test 换代 `test_iso1000_completeness_certified`。
- 数学零变更：iso100/trunc 仅 provenance 随 gen 哈希联动并同步 trunc `zero_source` 交叉引用，符合 v110 先例。
- 纪律边界：有限高度 T=1000 截断；区间见证层 PASS、kernel 层未证、非 RH 证据；隔离区间内区间见证 PASS、非全域声明。

未发现需要 REVISE 的具体缺口。判定：PASS。

已写入 `outbox/ANS-SEM-LABJUDGE-EXT16-cfts.md`，首行 PASS。

——cfts SI1语义轨·20261015T123005Z
