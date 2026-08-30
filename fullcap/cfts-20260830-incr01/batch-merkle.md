FULLCAP-BATCH-v1（增量批）
batch_id: INCR-01-cfts-20260830-001
line: cfts
session_scope: ['current-session']
range: T99..T107（全局续号，承接 FB01 T0..T98）｜ turn_seq_local 对照: 8..16
turn_count: 9
artifact_count: 21（turn 锚定）+ 3（事件轮 R15 锚定，无 TURN 节点）+ 7（本批产物，索引锚定防自指）
directive_id: FD01-cfts-20260828-001
scope: INCR
built_utc: 2026-08-30T07:48:31Z（date -u 实测）
builder: PI-cfts-R17-INCR-EXEC
merkle_root: cdcb619e8802ee702f03e6178e49cbdb328ab6e1584d023bdd522e9fba6ad47d
cursor_prev: cfts:cfts-lex-wave-20260828:T98@62a2b24996e84b5deb6ee3eae596bf99dcab240632357027cab889e490b3ff8b
cursor_next: cfts:current-session:T107@77e43b4023ed6c884ca79fa63d5c6792c3263337dcf5045e8425f14e9eb50888
batch_hash: e150933b4e50860697cc4a7178b8f0fd9bd67dcfbc59c1a8e0c028c295919d98
hash_rule: turn_hash=sha256(canon(q_raw)+canon(a_raw)+ts_utc+str(turn_seq))，canon=json.dumps(x,ensure_ascii=False,sort_keys=True)
merkle_rule: pairwise sha256(a+b)（hex 串拼接），奇数层末节点复制（与自身配对）；叶=turn_hash 升序（turn_seq 序）；本批叶集=T99..T107 九叶
batch_hash_rule: sha256(canon({batch_id, merkle_root, turn_hashes}))——FB01 batch_hash 规则未留档，本批自立规则并留档
session0_anchor（本批新 session）: {"session_id": "current-session", "turn_id": "cfts:current-session:T99", "ts_utc": "2026-08-28T21:00:00Z", "judge": "cfts", "候": "cisvr-rev", "basis": "session-current-raw.md turn_seq_local=8；承接 FB01 lex-wave 之同一会话续段", "note": "线级创世锚仍为 cfts:cfts-kernel-era:T0，不动"}

## turn_hash 清单（9）
T99 7fa5e62ba0d19a4f7e11987569c9419782423fa6d965cd95c5364bedc1ae7c96  cfts:current-session:T99  [local=8] [SUMMARY-DERIVED]
T100 e1992e1e63dac66eb8caed69cd3410091b2dc45f33bb9d267613f390710d82ce  cfts:current-session:T100  [local=9] [SUMMARY-DERIVED]
T101 9d86d78d6e0ab26442d6174c77367ff60b83d5a66f5a95ac7113a5800f6f2bcf  cfts:current-session:T101  [local=10] [RAW-VERBATIM]
T102 fd265560dee325f7b6303c63e16781ccc40375d48f70c5858938731298e6497a  cfts:current-session:T102  [local=11] [RAW-VERBATIM]
T103 e0b39c67df6be6fc2e1ab7aa38342d2fb33ad45a4651ddd38f83cee4fac23c4d  cfts:current-session:T103  [local=12] [RAW-VERBATIM]
T104 31154396dbd81fcab72c8c77186dc5c8ebc28fd4e1899d1934a455d987108ee7  cfts:current-session:T104  [local=13] [RAW-VERBATIM]
T105 cc3b1260b376e4d27a3a5bdb371bd8da8dcb5d6f58da3eb27fbd94a4bc030168  cfts:current-session:T105  [local=14] [RAW-VERBATIM]
T106 e7e45fac0d4150800893f4d190243243f83f06356c8b4018eeaa44eb2fb54c67  cfts:current-session:T106  [local=15] [RAW-VERBATIM]
T107 77e43b4023ed6c884ca79fa63d5c6792c3263337dcf5045e8425f14e9eb50888  cfts:current-session:T107  [local=16] [SUMMARY-DERIVED]

## 声明断点（不凑绿）
1. ts 全批 [derived]：静默期轮次零实测锚（FB01 段 D 曾有实测锚，本批无）；raw 件通配位（如 21:0xZ/01:4xZ）一律取下界 0 落定 ts_utc，逐轮 ts_provenance/ts_note 在案，不伪造具体分值。
2. ts 平点 1 处：T102=T103@2026-08-30T01:50:00Z（通配位下界相撞），顺序按源文件序保持。T106 答面通配位下界（07:20）早于其 q（07:22），ts_utc 取 q 推定 07:22:00Z，在案。
3. 答面保真分级：T99/T100=SUMMARY-DERIVED（原文在上下文压缩界前，要点转述）；T101..T106=RAW-VERBATIM（要点压缩）（raw 件原标注沿用，非逐字全文）；T107=在飞（本轮即 R17 构建轮）。
4. 「si/ 全五件」口径未合：vci-cfts/si/ 仓面实见 4 件（RETURN-CAPSULE/S-I-2-charter/S-I-3-charter/watch-log），第五件未定位——如实挂账，候 lead 指正或补件。
5. engine-state 系列 v3.0.0@T100/v3.1.0@T101 中间版未逐版留痕（远端 canonical=v3.2.0@T102 迁 vci-cfts）；ci-control INST-REG 若干版未逐版留痕（远端当前版在案；本地暂存件滞后，以远端回读为正）。
6. 迁移面 552 件逐件指纹在 MANIFEST FINAL（汇总锚=本地 research/migrate/MANIFEST.md，local-only 索引件）；注意 vci-cfts/MANIFEST.json 系 SHADOW-CI-01 仓面描述件，非迁移清单，勿混。
7. capgate.py/ledger.jsonl 本地件 local-only；ledger 为活账（闸链续增长），索引 sha=构建时点快照 49 行。
8. 事件轮 R15 三班产物 3 件（cfts-36/ROUTING-Q-18FILES/迁移 MANIFEST 锚）无 TURN 节点：跨锚对 PRODUCED_BY⇄YIELDED=21 对不含此 3 件，事件轮入 continuity/索引不入 turns（令规）。
9. watch-log.md 与 TH-SESCAP-01.md 为活件：索引/网络哈希=当前帖面（watch-log 含 seq0..seq9 至 07:37Z；TH-SESCAP-01 含 [6]@T100+[7]@T102）。
10. 本批 7 件产物不入 turn artifacts（防自指循环，FB01 先例），经 deliverables-index-add.json + 批次回件（ci-inbox session/cfts/inbox/INCR01-cfts-20260830-001.md）锚定。
11. FB01 界外 3 件（dm-queue/cfts 08-29 入站：USRM-HOLO-01/USRM-T5Q3-QKSA-01/USRM2CFTS-M3-01）非本线产物，不转入本批，仍候相应批次/线处置。
