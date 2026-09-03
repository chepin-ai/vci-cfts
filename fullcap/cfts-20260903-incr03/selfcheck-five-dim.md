# 复核五维自检报告（FULLCAP-cfts · INCR-03-cfts-20260903-001 增量批）

生成：2026-09-03T15:43:26Z（date -u 实测） ｜ 全部数值为本轮真跑代码复算所得（Python 3.12 / hashlib.sha256 / json canon=ensure_ascii=False,sort_keys=True）
复算入口：从**写入后**的 incr03/turns-incr.jsonl 逐行 json.loads 重算；跨批对照集=FB01 build/+INCR-01/02 落盘件。增量口径：本批只管 T113..T131 十九轮+其交付物增量；FB01/INCR-01/02 为已验基线（各经 lead 独立复算门 CLOSED-VERIFIED）。

## 维 1 ｜ 完整 —— PASS（声明断点 11 处，首条为实案疑案）

- turn_seq 连续无断：T113..T131 == range(113,132) 程序化全扫 ✅；cursor_prev 与 INCR-02 cursor_next **逐字一致**（T112@b5f177bd…）✅
- 交叉锚全互指：PRODUCED_BY 29 ⇄ YIELDED 29 对称差=**0** ✅（事件轮 8 件豁免+入站 2 件 null aid 注记，断点 7/8）
- mirror_state 覆盖：OK **44** / local-only **1**（capgate ledger 活链快照）/ PENDING **1**（自指 index）——合计 46 条与索引一致
- **实案挂账**：cfts-42/43/44/45/46 五件板面——watch-log/engine-state/供稿三面载「已发」，三仓树+全 commits 史核验零落（公告板止于 cfts-41）。自述落件 vs 仓面零落=T2-EXP-01「静默丢写」同型疑案本线实案，候 lead 裁定补发或核销（断点 1）。

## 维 2 ｜ 正确 —— PASS（零平点；两处区间估值声明）

- turn_hash 全量重算（19/19，=100%）：bad=[] ✅
- merkle_root 重算：b1e30270ed330a16… == 申报 ✅；batch_hash 重算：26bbe68ec40feb1c… == 申报 ✅
- ts_utc 单调：逆序 **0**、平点 **0**；全批 derived（供稿无逐轮戳，a 面锚=watch-log/verdict/run 实测戳逐轮在案）；**T126/T130 区间估值**取整点不伪造精确值（断点 3）。
- OTP/密钥纪律：递码七轮码值剜除复核 PASS（脚本断言五码值零出现于本批任何文本）；.kimi_session/qr.png 仅锚不录。

## 维 3 ｜ 唯一 —— PASS（批内+跨批双口径）

- 内容指纹：批内 19 轮 0 碰撞，与全链 113 轮（FB01 99+INCR-01 9+INCR-02 5）指纹集**零交集** ✅
- turn_hash：批内 0 碰撞，与全链 113 轮**零交集** ✅
- 交付物层：37 artifact_id 批内唯一，与 FB01+INCR-01+INCR-02 全量 artifact_id **零交集** ✅（入站 2 件 null aid 不占号）

## 维 4 ｜ 序号可复算 —— PASS

- 从 FB01 tip（TURN:cfts:cfts-lex-wave-20260828:T98）沿 INCR-01/02/03 NEXT 链重放：**33 步**抵达 tip `cfts:current-session:T131`，逐位 turn_seq==位置序号，MISMATCH 0 ✅

## 维 5 ｜ 创世锚唯一 —— PASS

- 本批无新 session：ANCHOR 边新增 **0** ✅（current-session 锚 T99 在 INCR-01 网唯一钉档；线级创世锚 kernel-era T0 不动）；cursor_prev≠SESSION-0 ✅

## 本交付自足数据

- 七件 sha16：turns-incr=9a74056f6d2ebf62｜余六件=（推送后批次回件清单为正；index 自指注记）
- Session-TN-incr state_digest=d6d70e9461e41aaf…（19 节点/67 边）｜File-TN-incr state_digest=25d4f022cefbfb22…（37 节点/66 边）
- merkle_root=b1e30270ed330a16e35c2384fb24fed4130cc8d412923229ceaccd9ab02cde3d｜cursor_next=cfts:current-session:T131@00c3593a7b9e4ac7175eb528dff0f9ca2c96615d385caf5e2974e3c66a0a2243
- 轮次分级：SUMMARY-DERIVED 19（处置锚档，lead 供稿制式；q 侧原话节选 RAW-VERBATIM，递码轮码值剜除）
