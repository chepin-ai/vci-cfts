# 复核五维自检报告（FULLCAP-cfts · INCR-01-cfts-20260830-001 增量批）

生成：2026-08-30T07:48:31Z（date -u 实测） ｜ 全部数值为本轮真跑代码复算所得（Python 3.12 / hashlib.sha256 / json canon=ensure_ascii=False,sort_keys=True）
复算入口：从**写入后**的 incr01/turns-incr.jsonl 逐行 json.loads 重算（非内存对象），merkle/batch_hash/双网 digest 同。增量口径：本批只管 T99..T107 九轮 + 其交付物增量，FB01（T0..T98）为已验基线（FB01 第三方复验 PASS 在案，watch-log seq8）。

## 维 1 ｜ 完整 —— PASS（声明断点 11 处）

- turn_seq 连续无断：T99..T107 程序化全扫 == range(99,108) ✅；cursor_prev 与 FB01 cursor_next **逐字一致**（T98@62a2b249…），批次咬合无缝 ✅
- 交叉锚全互指：PRODUCED_BY 21 ⇄ YIELDED 21，anchor_key=artifact_id+sha256 对称差=**0** ✅（事件轮 3 件无 TURN 节点，豁免声明=断点 8）
- mirror_state 覆盖：OK **27** / local-only **3**（capgate×2+迁移 MANIFEST 锚）/ PENDING **1**（deliverables-index-add.json 自指件，以批次回件清单为正）
- 断点清单（诚实标注）：batch-merkle.md「声明断点」1-11——ts 全 derived 零实测锚 / 通配位取下界 / 平点 1 处 / 答面要点压缩档 / si 第五件未定位 / engine-state·INST-REG 中间版未留痕 / capgate 活账快照 / 事件轮豁免 / 活件帖面哈希 / 自指产物锚 / FB01 界外 3 件仍挂。

## 维 2 ｜ 正确 —— PASS（ts 平点 1 处声明）

- turn_hash 全量重算（9/9，=100%）：bad=[] ✅
- merkle_root 重算：cdcb619e8802ee70… == 申报 ✅；batch_hash 重算：e150933b4e508606… == 申报 ✅（规则本批留档：sha256(canon({batch_id,merkle_root,turn_hashes}))）
- ts_utc 单调：逆序违例 **0**；**平点 1 处**（T102=T103@2026-08-30T01:50:00Z，通配位下界相撞）——顺序按源文件序保持，不伪造分数秒；ts_provenance 逐轮在案，通配位取下界规则全批一致，derived 项未洗白。
- T106 特例在案：答面通配位下界（07:20）早于其 q（07:22），ts_utc 取 q 推定，不取自相矛盾之下界。

## 维 3 ｜ 唯一 —— PASS

- 内容指纹 sha256(canon(q_raw)+canon(a_raw)) 全批 9 轮：**0 碰撞**；turn_hash 0 碰撞 ✅
- 交付物层：21 turn 锚定 artifact_id 唯一，且与 FB01 253 件 **零交集**（current-session 前缀）✅；事件轮 3 件 evt 前缀唯一；同路径多版（TH-SESCAP-01/engine-state/INST-REG/watch-log）以当前帖面 sha256 注记，非冲突。

## 维 4 ｜ 序号可复算 —— PASS

- 从 FB01 tip（TURN:cfts:cfts-lex-wave-20260828:T98）沿本批 NEXT 链重放：**9 步**抵达 tip `cfts:current-session:T107`，逐位 turn_seq==位置序号（99..107），MISMATCH 0 ✅

## 维 5 ｜ 创世锚唯一 —— PASS

- 本批新 session `current-session` × 1 session0_anchor（ANCHOR 边 1==1，T99@2026-08-28T21:00:00Z）✅
- 线级创世锚仍 `cfts:cfts-kernel-era:T0`（FB01 钉档，本批不动）✅；cursor_prev≠SESSION-0——本批为增量批非创世批，与 FB01 首批（cursor_prev=SESSION-0）口径区分在案 ✅

## 本交付自足数据

- 七件 sha16：turns-incr=674305c9fc53469d｜batch-merkle=（推送后批次回件清单为正）｜continuity=（同）｜session-tn-incr=（同）｜file-tn-incr=（同）｜index=（自指注记）｜selfcheck=（同）
- Session-TN-incr state_digest=0d28bf5facd7925c…（10 节点/40 边）｜File-TN-incr state_digest=fba46e77e1bb39bf…（24 节点/45 边）
- merkle_root=cdcb619e8802ee702f03e6178e49cbdb328ab6e1584d023bdd522e9fba6ad47d｜cursor_next=cfts:current-session:T107@77e43b4023ed6c884ca79fa63d5c6792c3263337dcf5045e8425f14e9eb50888
- 轮次分级：RAW-VERBATIM 6（要点压缩档含）/ SUMMARY-DERIVED 3（T99/T100/T107 在飞）
