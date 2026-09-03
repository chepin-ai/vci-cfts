FULLCAP-BATCH-v1（增量批）
batch_id: INCR-02-cfts-20260901-001
line: cfts
session_scope: ['current-session']（同会话续段，无新 session）
range: T108..T112（全局续号，承 INCR-01 T99..T107）｜ turn_seq_local 对照: 17..21
turn_count: 5
artifact_count: 16（turn 锚定）+ 6（事件轮/外部锚，无 TURN 节点）+ 7（本批产物，索引锚定防自指）
directive_id: FD01-cfts-20260828-001 ｜ 本拍令：root「继续SI1～4」（2026-09-01T18:35Z【derived】）
scope: INCR
built_utc: 2026-09-02T02:12:11Z（date -u 实测）
builder: PI-cfts-R17-INCR-EXEC（S-I/3 线续转）
merkle_root: 5acfe1abc1deb3d02381069866a311938578d5ecbdef0c6f8f3bfcb934051019
cursor_prev: cfts:current-session:T107@77e43b4023ed6c884ca79fa63d5c6792c3263337dcf5045e8425f14e9eb50888
cursor_next: cfts:current-session:T112@b5f177bd99c1d7303031369aea9b6ffaa20971d9b91a45bcaae5c7a3a326f0d5（至 T112 构建拍，T112 轮在飞）
batch_hash: aa5dbe190847bc039335bd47c9ad960bb1441a6dacf10514932ab8d8175027a4
hash_rule: turn_hash=sha256(canon(q_raw)+canon(a_raw)+ts_utc+str(turn_seq))，canon=json.dumps(x,ensure_ascii=False,sort_keys=True)
merkle_rule: pairwise sha256(a+b)（hex 串拼接），奇数层末节点复制（与自身配对）；叶=turn_hash 升序（turn_seq 序）；本批叶集=T108..T112 五叶
batch_hash_rule: sha256(canon({batch_id, merkle_root, turn_hashes}))（INCR-01 自立规则沿用）
q_raw 供稿面：lead 直读会话原文逐字符供稿（权威面）；T110 root 原文作「ursm」逐字照录不规整化；T112 全角波浪号 U+FF5E 原样；T110 附图（PNG 2240×238）不入 q_raw 本体，ts_note 在案。

## turn_hash 清单（5）
T108 a18a45e8b0007ba4b9654e3b3c64c555ff9623bcdc82ee5eb9c7f3dd04c376ec  cfts:current-session:T108  [local=17] [RAW-VERBATIM]
T109 b42881e090c53a4c49a7667b26ecbaacd443141da5413a778047ea7abd1e3c13  cfts:current-session:T109  [local=18] [RAW-VERBATIM]
T110 2716e15d6b9ca661dca37a63da08e93940f6be8dbc41339c56e0e1836ba6172f  cfts:current-session:T110  [local=19] [RAW-VERBATIM]
T111 9933e4f6a623a8af1a3cedb08ff2a196f162b5ca996b14f16ba42744e80b3df2  cfts:current-session:T111  [local=20] [RAW-VERBATIM]
T112 b5f177bd99c1d7303031369aea9b6ffaa20971d9b91a45bcaae5c7a3a326f0d5  cfts:current-session:T112  [local=21] [在飞→SUMMARY-DERIVED]

## 声明断点（不凑绿）
1. ts 全批 [derived] 零实测锚（同 INCR-01 口径）；无通配位（lead 供稿落定到秒）；平点 0 处；T109 q/a 同拍同戳（09:00Z，源序保持，在案）。
2. 答面保真：T108..T111=RAW-VERBATIM（要点压缩）（a 面要点以 watch-log seq11..14/engine-state META-TICK-16..19 在案件为据）；T112=在飞（本轮即 R17 INCR-02 构建轮）。
3. 会合拍轮数裁定：lead 裁定会合拍=1 轮（「睁眼」后 root 下一条即「继续」，中间无第二条 root 消息；watch-log seq11 一记即全部）——本批 T108..T112 共 5 轮（初拟 T108/T109 拆分不成立，构建前已由 lead 裁定修正，零返工入链）。
4. 活件快照 3 件（engine-state v3.2.0 META-TICK-20/watch-log seq0..15/INST-REG 四条同步）：索引 sha=构建时点远端回读快照，宿主续写则远端新于索引——以快照注记为诚实口径；中间版（META-TICK-16..19/INST-REG 若干版）未逐版留痕。
5. 事件轮/外部锚 6 件无 TURN 节点：cfts-37/cfts-38（静默期 host 值守公告）、CFOS-NORTHSTAR-01（R18，T107 派出静默期交付）、pattern-dossier（R16，local-only）、chsh-01-wave47.json（usrm 外部证据锚，只锚不占）、capgate ledger（local-only 活链 49→72 节）；跨锚对 PRODUCED_BY⇄YIELDED=16 对不含此 6 件。
6. OTP_PHONE/OTP_EMAIL1/OTP_EMAIL2/LONGCAT_API_KEY：密钥值永不入任何文本（q_raw 仅名面）；〈RED〉 仓位差候 root 改挂 vci-cfts（事件轮在案）；自证拍 run 33542104292 completed failure=预期内缺口文档化。
7. 值守机检背景层（weave/duty、pulse 新件 09-01 起 ~30 件）不入本批索引——机器台账层非本批会话交付物，链上自洽（duty.log/state.json 在仓）。
8. SYN3-ESCALATE@08-31T02:32Z 届时仍零→升级帖 cfts-39 未发：因 usrm W70 代执行关闭（T110 在案），升级条件被事件消解，非漏发。
9. 本批 7 件产物不入 turn artifacts（防自指循环，FB01/INCR-01 先例），经 deliverables-index-add.json + 批次回件（HUB-MAIL session/cfts/inbox/INCR02-cfts-20260901-001.md）锚定。
10. T110 附件（W72 判词截图 PNG）本体不入链（二进制会话附件无可及存储径），内容摘要单行经 ts_note 注记；判词正本 ci-control/bridge/adjudications/XLINE-DISPOSITION-W72-01.md 在仓可验。
