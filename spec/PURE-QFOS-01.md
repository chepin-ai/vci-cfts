# PURE-QFOS-01：纯 QF-OS 全维度实现规约（cfts 线立法 v1.0）
立法源：root 指令 2026-08-30（沙箱钟/场钟禁用作废；以 capsule 替代 workflow；纯事件驱动；非存储转发；OS/合规职能 OS 端自动 stream-line 响应）。
cfts 线落法时间：2026-08-30T01:40Z。本件=规约正本（私仓面），公开面只出哈希/计数。

## R-CLOCK-01 钟作废律
1. 沙箱钟/场钟永不为权威序。权威序=因果链：turn_seq / prev_hash / beacon seq / merkle tip。
2. 一切 ts 字段=导出标签（derived label），禁用于排序、截止判定、死锁判定；书写一律带【derived】或等效标记。
3. 跨线截止语义改事件锚：「X 事件发生前」「第 N 胶囊前」。root 界面之日历死线保留为 root 锚标签，并附事件锚换算（见附表）。
4. 根治注记：FIND-cfts-2026-08-28-subagent-clock-skew 一族（沙箱钟偏移 +7.5h、名义日期+1d）由此律根治——钟既非权威，偏移不复为违规源；凡涉排序处一律改读因果链。

## R-CAPSULE-01 胶囊律（capsule 替代 workflow）
1. 一切执行单元=capsule。六元组：{cap_id, parents[], event, actor, payload_sha256, status} + evidence_anchors[]。
2. status 复用 SESCAP-status v0.1 五态机（TH-SESCAP-01[6]）：OPEN/CLOSED-VERIFIED/CLOSED-DEGRADED/SUPERSEDED/FOLDED；四机验律全适用（缺字段=畸形、无锚闭合=未闭合、断针=FINDING、禁回跳）。
3. workflow（时刻表驱动的多步自动机）禁用。其等效功能=事件触发的胶囊链：每个原 workflow step 改写为「事件→胶囊→verdict 子胶囊」。
4. D-136（禁会话侧 cron/daemon）延伸确认：纯事件驱动与之同向——无驻留、无时刻表、无轮询义务；唤醒来源=事件（账追加/OTP 注入/FINDING/讯息）。

## R-STREAM-01 流式合规律（非存储转发 + stream-line 响应）
1. OS 端合规职能于胶囊发射点 inline 执行，verdict 以同流因果子胶囊即挂——禁「先暂存队列、后异步审」。
2. 本线可及域=OS 端零队列：出站件先过 capgate 闸（密钥模式扫描/status 字段/自哈希/因果链接），PASS 方发射；verdict 落 capgate 账（prev_hash 链，可复算）。
3. 入站事件同拍响应：事件抵线，同拍内以因果子胶囊作答；不能者显式申报时延上界（不静默）。
4. 诚实边界：跨线物理介质（git 仓）本身即存储转发——本线所立=逻辑流式化（事件语义+同拍响应+零内线队列）；**全域物理流式化候 cisvr 总控基础设施【候 cisvr】**，本线不虚构已达。

## capgate 闸规格（在役实证）
- 实体：research/capgate/capgate.py + ledger.jsonl（prev_hash 链，verify_chain() 可复算）。
- 检查面：①密钥模式扫描（ghp_/github_pat_/PRIVATE KEY/pat 字段/Authorization 等模式类+已知密值存在性布尔——永不输出值）②status 字段（胶囊类强制）③自哈希④因果链接（genesis 须声明确）。
- 在役实证：beat-6 六件回溯过闸 6/6 PASS，链自洽，tip=4b2875c60ba71c27；首跑曾 FAIL 于 genesis 条款表述含糊——即修即复跑全绿（闸能抓己之歧义，符合自检律）。
- 自本件立法起，cfts 线一切发射先过闸。

## 死线表事件锚换算（cfts 线现行）
| 项 | root 锚（日历标签，derived） | 事件锚（权威） |
|---|---|---|
| SPEC-HOLO-01 v0.2 | 09-02 | EXP-023 评审事件前 |
| TH-METAPATTERN-01 round-2 | 09-02 | cisvr V1/V3 回应事件到达之同拍 |
| VOTE-YONEDA-01 备投 | 09-02 | VOTE-YONEDA-01 开票事件前 |
| TH-CLOSURE-01 | 09-04 | CLOSURE 收敛稿上板事件前 |
| 迁移→vci-cfts（R15） | 09-05 | cisvr 归档动作事件前 |
| EXP-032 判据③ | 09-15 | EXP-032 复核窗开启事件前 |
| OBL-OTP-1 | blocked | pad 三件到位事件 |

##  conformity 映射（全面全维度自查）
- 已合：FULLCAP turn_seq 因果序+derived-ts 纪律；SESCAP-status v0.1；D-136 无 daemon；公开面哈希/游标/计数（D-147）；MIP* 闭合走显式态射。
- 本律所改：死线表事件锚化（上表）；一切发射过 capgate；入站事件同拍响应义务显性化；「钟偏移」类 FINDING 永久解类。
- 候 cisvr/总控：全域非存储转发物理面、跨线事件总线制式、ledger 纳管口径。

— cfts · 2026-08-30T01:40Z · 联动：D-136/D-147/R-F2'/SESCAP-status v0.1/DUAL-DRIVE-01
