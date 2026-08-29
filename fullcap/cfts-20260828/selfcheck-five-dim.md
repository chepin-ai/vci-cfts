# 复核五维自检报告（FULLCAP-cfts · FB01-cfts-20260828-001）

生成：2026-08-29T01:55:24Z（date -u 实测） ｜ 全部数值为本轮真跑代码复算所得（Python 3.12 / hashlib.sha256 / json canon=ensure_ascii=False,sort_keys=True）
复算入口：从**写入后**的 build/turns-raw.jsonl 逐行 json.loads 重算（非内存对象），merkle/batch_hash 同。

## 维 1 ｜ 完整 —— PASS（声明断点 9 处）

- turn_seq 连续无断：T0..T98 程序化全扫 == range(99) ✅
- 交叉锚全互指：PRODUCED_BY 253 ⇄ YIELDED 253，anchor_key=artifact_id+sha256 对称差=**0** ✅
- mirror_state 覆盖：OK **151** / PENDING **102**（PENDING 逐件 mirror_note 在案：GitHub 单向在案 / 本地未推 / 帖面多线演进 / 自指产物）——OK 全覆盖不成立之处=声明断点 5
- 断点清单（诚实标注）：见 FB01 批次文件「声明断点」1-8 + continuity.md 缝隙 1-9（同构）；另：kernel-era T0 内容层断（D4 延迟锚）、duty/outbox 90 轮问答原文不可得（LEDGER-DERIVED 兜底）。

## 维 2 ｜ 正确 —— PASS（ts 平点 5 处声明）

- turn_hash 全量重算（99/99，超 ≥10% 要求）：bad=[] ✅
- merkle_root 重算：76f2a79a9a76868a… == 申报 ✅；batch_hash 重算：9ce2da7d97c8f34f… == 申报 ✅
- ts_utc 单调：逆序违例 0；**平点 5 处**（recs[74,75]=slA[15,16]@2026-08-27T20:06:19Z；recs[78,79]=slA[19,20]@20:58Z；recs[82-85]=sl9[0-3]@2026-08-28T07:40Z）——台账批量同戳写入，顺序按源数组序保持，不伪造分数秒；ts_provenance 逐轮在案（measured/derived/ledger 分级），lex-wave derived 项未洗白。
- 时钟面差异 ~10h（dashboard 台账 vs lex-wave derived 对同事件组）：两源原样保留，declare 不对齐。

## 维 3 ｜ 唯一 —— PASS

- 内容指纹 sha256(canon(q_raw)+canon(a_raw)) 全批 99 轮：**0 碰撞**；turn_hash 0 碰撞 ✅
- 交付物层：253 artifact 按 artifact_id 唯一；同内容多实例（如 harvest 副本）以同 sha256 注记，非冲突。

## 维 4 ｜ 序号可复算 —— PASS

- 从 Session-0 锚（TURN:cfts:cfts-kernel-era:T0）沿 NEXT 链重放：98 步抵达 tip `cfts:cfts-lex-wave-20260828:T98`，逐位 turn_seq==位置序号，MISMATCH 0 ✅

## 维 5 ｜ 创世锚唯一 —— PASS

- 4 session × 各 1 session0_anchor（ANCHOR 边 4==4）：kernel-era T0（线级创世，git 真根 702bfe9b/09b3e65c 双 sha 注记）/ duty-era T5→**修正为 T1**（首拍 pulse 20260818-060921，构建中发现锚定错位即修，修正迹留档）/ outbox-era T57 / lex-wave T89 ✅
- cursor_prev=SESSION-0 与首批吻合 ✅；锚一经钉档永不改（kernel-era 锚经 lead 裁决按真根钉档）。

## 修正迹（轮询回测律/分枝互证工作证据，不得删改掩饰）

1. lead 盘点原引 Session-0 候选「396823805e0b @2026-08-12T01:54:24Z」；本构建 `git cat-file -p` 实证其有 parent a92154f1 **非根**（采样法错误：log --reverse --max-count 先取新件），向下修正至真根 702bfe9b @2026-08-07T13:30:02Z（local）/ 09b3e65c（remote，同日期同 message，history_rewritten=true）。lead 裁决：批准修正按真根推进。
2. duty-era session0_anchor 初绑 T5（首 duty 班），复核发现 T1（pulse 首拍 08-18T06:09Z）更早，即修正重钉。

## 本交付自足数据

- 六件 sha16：turns-raw=5e00881e5b8ac601｜FB01=9ba38ce51210ec01｜continuity=8d9d89f744f43828｜session-tn=cca01221deae3927｜file-tn=b45e4445fefa0e36｜index=（推送后批次回件清单为正，自指注记）
- Session-TN state_digest=a023920ba4008f78…（104 节点/458 边）｜File-TN state_digest=bf4e8edb3195ed28…（262 节点/659 边）
- merkle_root=76f2a79a9a76868a158ce8f7c19cb4440b56e94da13fc132ef50121189f8d52c｜cursor_next=cfts:cfts-lex-wave-20260828:T98@62a2b24996e84b5deb6ee3eae596bf99dcab240632357027cab889e490b3ff8b
- 轮次分级：RAW-VERBATIM 4 / SUMMARY-DERIVED 4 / LEDGER-DERIVED 90 / UNAVAILABLE-GAP 1
