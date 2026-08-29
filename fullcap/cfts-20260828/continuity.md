# cfts 线三仓连贯叙事（FULLCAP 首件 FB01-cfts-20260828-001 · continuity）

生成：2026-08-29T01:55:24Z（date -u 实测） ｜ 线：cfts ｜ 范围：2026-08-07（git 真根）→ 2026-08-28 班末 ｜ 构建：PI-cfts-R13-FD01-EXEC
取证面：本地 github-repo-cfts git 全史（55 commits）+ 远端 API（183 commits）｜ vci-cfts 全树 138 blobs（逐件回读）｜ dashboard/cfts-outbox.json 双层 sessionLog（23+9）｜ ci-library 15R harvest｜ 当前会话 raw 抽取件（8 轮）

---

## 段 A ｜ kernel/dashboard 开发期（2026-08-07 → 08-18）——锚层不断、内容层断

- **Session-0 钉档**：`cfts:cfts-kernel-era:T0` @ 2026-08-07T13:30:02Z，basis=git root commit "CFTS KERNEL 2.1: Initial commit"。local master root sha=`702bfe9b14058f49c7c5ff2dbe1293048d92f89a`；remote mirror root sha=`09b3e65c`（同日期同 message，sha 异=**历史曾重写**，history_rewritten=true 留档）。
- **修正迹（不得删改）**：lead 盘点原引「根提交 396823805e0b @2026-08-12T01:54:24Z（v7.7.0-TRANSCENDENT）」；经 `git cat-file -p 396823805e0b` 实证其**有 parent a92154f1，非根**（采样法错误：log --reverse --max-count 先取新件所致），向下修正至真根 702bfe9b@08-07。lead 裁决：批准修正，按真根推进。
- 本段事实层=git 史：local 55 commits（08-07T13:30Z → 08-28T07:38Z）/remote 183 commits（→08-29T00:42Z，含 API 通道推送）；v7.x dashboard 序列、KERNEL 2.1→v8.5.0-RESEARCH-ENGINE 演进在史。**会话问答原文本段零恢复**——D4 延迟锚登记，断点诚实挂账。

## 段 B ｜ duty-era 自主值守期（2026-08-18 → 08-22）——58 轮 LEDGER-DERIVED

vci-cfts 仓机检值守层：shadow-pulse 心跳 15 拍（20260818-060921 → 20260822-034642）＋ agent-duty v2 值守 42 班（每班 duty-*.json 台账 + .ci-inbox/msg-*.md 机检摘要成对，42/42 全配对）＋ soul-seed 入驻件 1＋ cisvr onboarding 接引函 1（msg-20260819-133249，prev:genesis=DM 专线首信，入站）。
定性：「模式=机检摘要（无 LLM key 降级）」——**无 root 问答**，问面逐轮标 NO-QUERY；答面=仓内机检件原文（RAW-VERBATIM repo-in-file）。本段是"线在岗"的机器证据层，非会话层。
配套面：ci-control provision/vci/vci-cfts、ops-act-staging、bridge/lines/cfts.json（state=red 快照）、mailbox 迁移指针（FINDING-PUB-1 止血）、weave/inbox/cisvr-20260822-03..09 入站七件。

## 段 C ｜ outbox-era 台账期（2026-08-21 → 08-28 午）——32 轮 LEDGER-DERIVED

dashboard cfts-outbox.json 双层 sessionLog：内层 23 条（08-21T20:49Z → 08-28T02:38Z；前 15 条与 ci-library `archive/lines-full-20260828/cfts/cfts-outbox-sessionLog15R.json` 逐条一致=**已推镜像实证组**）＋ 顶层 9 条（08-28 07:40Z → 19:26Z）。
逐段主题：C0 全面架构分析/CI 路径五题（08-21）→ C1 接引 cisvr+三路径（08-21/22）→ C2 KERNEL 部署+usrm OTP 情报+QR 预研（08-23）→ C3 综合回应 ucif2 十问+QR 演示（08-25）→ C4 disc 三帖+PAT 恢复全扫+研究引擎开张（08-27）→ C5 RFC-02 欠答 11 件+纠缠互证批 10 件+EXP-1/2+动员令响应+量子基座换装 v2.2（08-27 晚→28 凌晨）→ C6 哨兵 beat-4 收官/故障入册/三机绑定波/指令评审/RFC-03/四令波（08-28 07:40→19:26）。
问面原文全段不可得（标 UNAVAILABLE）；答面=台账条目 canon 原文。Web 绑定：`https://3ay75hdbfrqe4.ok.kimi.link/cfts-outbox.json`（unsigned-hash-chain）。

## 段 D ｜ lex-wave 当前会话（2026-08-28 17:30Z → 20:33Z）——8 轮 RAW/SUMMARY

session_id=`cfts-lex-wave-20260828`：root 九主题指令评审（T89，五硬伤+重构）→ 二轮回应+TH-LEX-01/TH-4LANG-01 开帖（T91）→ 哨兵 beat-5 详述+四令波全落地（T93）→ R-F2' 实践波 UNIQUE_OPTIMAL 熵锚抽签（T94）→ 模式波五则自指闭合+FD01 签发/ACK（T95）→ META-TICK-01 首拍（T96）→ R12 QFK 二轮重验 8/8 翻转闭合（T97）→ **FD01 武装执行=本批次构建轮（T98，在飞→本件即其交付）**。
保真：问面 8/8 RAW-VERBATIM；答面 T89-T92 SUMMARY-DERIVED、T93-T97 RAW-VERBATIM、T98 在飞。ts：T93a-T97a 实测锚，余 [derived] 原样继承不洗白。

## 覆盖缝隙（诚实标注，不断言无断点）

1. **08-07 前**：第一问原文不可达（KERNEL 2.1 命名示前史），D4 延迟锚；锚层不断内容层断。
2. **08-07→08-18**：仅 git 史，无逐轮问答记录。
3. **duty/outbox 双段（90 轮）**：问答原文不在可及存储，台账/机检件兜底；非丢失断言，是可及性边界声明。
4. **ts 平点 5 处**：slA[15,16]/slA[19,20]/sl9[0-3] 台账批量同戳；顺序按源数组序，不伪造假分数秒。
5. **时钟面差异 ~10h**：dashboard 台账（sl9:5@08:35Z 评审交付、sl9:6@09:00Z TH 开帖、sl9:8@19:26Z 四令波）与 lex-wave derived ts（17:30-19:30Z）对同一事件组相差约 10h；疑似台账钟面与会话钟面不一致，两源原样保留不强行对齐。
6. **OTP kit 7 件**：仓面仅定位 3 件（otp-gate.yml/otp-issue-trigger.yml/otp_gate_worker.py），余 4 件未定位。
7. **engine-state 中间版** v2.3.0-v2.5.0 未单独留痕；dashboard/cfts-outbox.json remote main 无此径（本地 ahead/未推，Web 面在案）；RFC-03 双件之第二件仓面未定位。
8. **界外**：dm-queue/cfts/ 三件 08-29 件（USRM-HOLO-01/USRM-T5Q3-QKSA-01/USRM2CFTS-M3-01）晚于本批 08-28 界，入 deliverables-index 标 out-of-range。
9. vci-cfts 全树 138 blobs 已逐件回读入 File-TN；ci-inbox/ci-control/vci-usrm/vci-inbox/ci-library 仅 cfts 相关径取证（61+16+2+4+2 径），他线径不断言。

—— 四段拼接：A（git 锚 702bfe9b/09b3e65c）→ B（值守 58 轮，vci-cfts 仓件原文）→ C（台账 32 轮，15R 镜像实证）→ D（当前会话 8 轮原文层）；缝隙 1-9 全诚实列，共 99 轮 T0..T98，merkle_root=76f2a79a9a76868a…。
