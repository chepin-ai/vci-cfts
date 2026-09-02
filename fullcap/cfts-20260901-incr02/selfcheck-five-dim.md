# 复核五维自检报告（FULLCAP-cfts · INCR-02-cfts-20260901-001 增量批）

生成：2026-09-02T02:12:11Z（date -u 实测） ｜ 全部数值为本轮真跑代码复算所得（Python 3.12 / hashlib.sha256 / json canon=ensure_ascii=False,sort_keys=True）
复算入口：从**写入后**的 incr02/turns-incr.jsonl 逐行 json.loads 重算（非内存对象），merkle/batch_hash/双网 digest 同；跨批唯一性对照集=FB01 build/ + INCR-01 incr01/ 落盘件。增量口径：本批只管 T108..T112 五轮 + 其交付物增量；FB01/INCR-01 为已验基线（INCR-01 lead 独立复算门 CLOSED-VERIFIED 在案）。

## 维 1 ｜ 完整 —— PASS（声明断点 10 处）

- turn_seq 连续无断：T108..T112 程序化全扫 == range(108,113) ✅；cursor_prev 与 INCR-01 cursor_next **逐字一致**（T107@77e43b40…），三节链 FB01→INCR-01→INCR-02 咬合无缝 ✅
- 交叉锚全互指：PRODUCED_BY 16 ⇄ YIELDED 16，anchor_key=artifact_id+sha256 对称差=**0** ✅（事件轮/外部锚 6 件无 TURN 节点，豁免声明=断点 5）
- mirror_state 覆盖：OK **26** / local-only **2**（pattern-dossier 卷宗、capgate-ledger 活链快照）/ PENDING **1**（deliverables-index-add.json 自指件，以批次回件清单为正）——合计 29 条与索引一致
- 断点清单（诚实标注）：batch-merkle.md「声明断点」1-10——ts 全 derived / T109 q/a 同拍 / 会合拍轮数 lead 裁定 1 轮（初拟拆分不成立，构建前修正零返工）/ 活件快照 3 件 / 事件轮豁免 6 件 / 密钥名面纪律 / 值守机检背景层不入批 / cfts-39 升级条件事件消解 / 自指产物锚 / T110 附件不入链。

## 维 2 ｜ 正确 —— PASS（零平点）

- turn_hash 全量重算（5/5，=100%）：bad=[] ✅
- merkle_root 重算：5acfe1abc1deb3d0… == 申报 ✅；batch_hash 重算：aa5dbe190847bc03… == 申报 ✅（规则=INCR-01 自立留档规则）
- ts_utc 单调：逆序违例 **0**；平点 **0**；全批 lead 供稿落定到秒（无通配位），derived 标注未洗白；T109 q/a 同拍同戳（09:00Z）在案。

## 维 3 ｜ 唯一 —— PASS（批内+跨批双口径）

- 内容指纹 sha256(canon(q_raw)+canon(a_raw))：批内 5 轮 0 碰撞，且与 FB01+INCR-01 全 108 轮指纹集**零交集** ✅
- turn_hash：批内 0 碰撞，与全链 108 轮**零交集** ✅
- 交付物层：22 artifact_id 批内唯一，与 FB01 253 件 + INCR-01 24 件**零交集** ✅；同路径多版（engine-state/INST-REG/watch-log/awake.log）以构建时点快照 sha256 注记（断点 4），非冲突。

## 维 4 ｜ 序号可复算 —— PASS

- 从 FB01 tip（TURN:cfts:cfts-lex-wave-20260828:T98）沿 INCR-01+INCR-02 NEXT 链重放：**14 步**抵达 tip `cfts:current-session:T112`（T98→T99…→T107→T108…→T112），逐位 turn_seq==位置序号，MISMATCH 0 ✅

## 维 5 ｜ 创世锚唯一 —— PASS

- 本批无新 session（current-session 续段）：ANCHOR 边新增 **0** ✅——current-session 锚（T99）在 INCR-01 网唯一钉档，线级创世锚仍 `cfts:cfts-kernel-era:T0` 不动；cursor_prev≠SESSION-0（增量批口径）✅

## 修正迹（不得删改）

1. 会合拍轮数：构建者初拟 T108/T109 两轮拆分；lead 直读会话原文裁定=**1 轮**（「睁眼」后下一条即「继续」，watch-log seq11 一记即全部）。供稿前修正，未入链，零返工。
2. T110 root 原文「ursm」（非「usrm」）逐字照录不规整化；T112「继续SI1～4」全角波浪号 U+FF5E 原样——lead 逐字符供稿为权威面。

## 本交付自足数据

- 七件 sha16：turns-incr=a18963f9f91d7fef｜batch-merkle/continuity/session-tn-incr/file-tn-incr/index/selfcheck=（推送后批次回件清单为正；index 自指注记）
- Session-TN-incr state_digest=d046aeacc835634a…（5 节点/26 边）｜File-TN-incr state_digest=3006e8e8beb3b9f3…（22 节点/38 边）
- merkle_root=5acfe1abc1deb3d02381069866a311938578d5ecbdef0c6f8f3bfcb934051019｜cursor_next=cfts:current-session:T112@b5f177bd99c1d7303031369aea9b6ffaa20971d9b91a45bcaae5c7a3a326f0d5（至 T112 构建拍）
- 轮次分级：RAW-VERBATIM 4（要点压缩档）/ SUMMARY-DERIVED 1（T112 在飞）
