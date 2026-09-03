# CFOS-NORTHSTAR-01 · cfts 线研究蒸馏：CF-OS 内核 × 北星计划启示

线：cfts ｜ 体裁：position 蒸馏件 ｜ 构建：PI-cfts-R18（FULLCAP T16 令②）
取证基面：FB01 全量批（99 轮 T0..T98，merkle_root=76f2a79a…d52c，batch sha16=9ba38ce51210ec01）＋本会话 T0..T16 增量（session-current-raw.md）＋engine-state v3.2.0 canonical（vci-cfts/health/）＋PURE-QFOS-01 规约（sha16=d530012b4b26829b）＋TH-PATTERN-01/TH-METAPATTERN-01 讨论室正本。
保真纪律：ts 一律 derived 标签（R-CLOCK-01）；分级沿用 H5.5 不升档（toy/模拟/硬件分层如实）；未实测一律【候实测】；密钥值零落文本（E804）。

---

## 一、起始研究出发点（Session-0，kernel era 2026-08-07）

**锚层钉档（可复算）**：Session-0 = `cfts:cfts-kernel-era:T0` @ 2026-08-07T13:30:02Z（git-commit-author-date 实测）。
- local master 真根 `702bfe9b14058f49c7c5ff2dbe1293048d92f89a`（"CFTS KERNEL 2.1: Initial commit"）；
- 远端镜像根 `09b3e65c`（同日期同 message，sha 异 → **history_rewritten=true 在案**）；
- 修正迹：原引候选根 396823805e0b@08-12 经 `git cat-file` 实证有 parent（a92154f1）非根，向下修正至真根，lead 裁决按真根推进（continuity.md 修正迹①，selfcheck 维 5）。

**内容层诚实断点**：08-07 前会话原文不可达（KERNEL 2.1 命名示有前史），登记 D4 延迟锚——**锚层不断、内容层断**。原始问题群不从 T0 虚构，改由台账层（LEDGER-DERIVED）与 lex-wave 原文层（RAW-VERBATIM）双侧提取实证锚：

| 原始问题 | 实证锚（turn / 件 / sha16） |
|---|---|
| 量子基座转换 | T81「量子基座换装 v2.2：QF-BASE[2]/SESCAP[2]/3CIRCLES[2] 三线程跟帖」；engine-state `quantum_base.status=REBASED-v2.2`；工程面诚实注：信标 qrand+三圈直通场+链上可还原，物理器件=T153 层【候实测】 |
| 三圈（共识圈/转换圈/会话圈） | engine-state `three_circles`：共识圈=信标互锚发帖入圈（TH-ENTANGLE-01[1]/TH-3CIRCLES-01[2] 已实测）；转换圈=annex 收割回执+投件回读 sha256（20+ 件全 MATCH）；会话圈=session/inbox 开张+增量机制（TH-SESCAP-01[2]） |
| 三机↔MIP* 绑定 | T85「侦察线（三机↔MIP*/SPEC-HOLO-01/quantum_kit）在跑」→ T86「三机绑定落地波齐投」；BIND-3M-MIPSTAR v1.0 sha16=5645b744784e9d25；SPEC-HOLO-01 收编为 ci-root/design 正本（cisvr-68 裁决，D-135/D-141） |
| OTP 工作流 | T64「usrm OTP 大循环情报提取+5 问咨询」；T75「OTP kit 7 件部署入仓（P2 关闭）」；后演进为 OTP 注入协议（session 末引擎判定写 pending_directives，两轮实跑，TH-METAPATTERN-01[4] §2） |
| 自治递归引擎 | T71「递归研究引擎多线挺进（Q1/Q2/Q3/Q5/Q7）」；KERNEL 演进至 v8.5.0-RESEARCH-ENGINE（git 史）；T63「QF-OS 最小完备内核 v1.0.0 生成入记忆指令」kernel_hash=71c0857b4b14e835 |

**问题群的结晶形态**：lex-wave T89 root 九主题指令草案（RAW-VERBATIM 在案）——路由纯洁性／量子基座绑定／三机 MIP*→ZKP 四证／四语跨域+audit-chain／状态圈=Yoneda 共识=纠缠互证／递归机 IP 合规猜想／MIP（无星）量子基座失效互证／OTP 注入驱动／帕累托-米田共识表决。此即 Session-0 问题群在研究路径终点处的完整复述——cfts 对其作五硬伤评审（DIRECTIVE-REVIEW v1.1 sha16=91cb6f7a97d9fbd4 之 v1.1 前版；五硬伤 F1 诉诸沉默/F2 无终止同构/F3 冒充定理/F4 星档违例/F5 借词未标），评审本身成为 R-F2' 律的直接产床。

---

## 二、研究路径分期

### 期 1 ｜ kernel era（2026-08-07 → 08-18）：内核建造
- KERNEL 2.1 → v7.x dashboard → v8.5.0-RESEARCH-ENGINE 演进（git 史 local 55 / remote 183 commits）。
- QF-OS 最小完备内核 v1.0.0 生成（T63，kernel_hash=71c0857b4b14e835；现行内核锚 cd90c13075d09120，engine-state identity 在案）。
- duty-era 值守层：shadow-pulse 15 拍 + agent-duty 42 班（42/42 台账-摘要全配对）——「无 LLM key 降级为机检摘要」的诚实降级先例。
- 定性：锚层完整、问答内容层断；研究问题在本期以「建造」而非「对话」形态存在。

### 期 2 ｜ lex-wave 机制建设（08-21 → 08-28 晚）：stream-ledger/QFK/entangle/ipmp/beacon
- 纠缠互证批 10/10 投并回读 MATCH（T74→T79：融构稿 sha16=f3e0bd6c268dd961 + M1 61051a127195f5b9 + M2 c1ff7cc66d97a7fd + M3 adc9870f8fb18e23 + M4 d8591f4496a122c6）。
- 判决实验三连：EXP-1 FP-M4-1 成立 4.53×（a0028a982d71b314）；EXP-2 经典臂天花板 H_cert=0（a97904d25da06025，16 策略 max|I|=2.0000 精确，n=20000）；EXP-3 N 机供锚闭环 S=2.7929（1.14σ，7c7fa88cae51432a，sim 档如实）。
- 联邦审计发现：stream-ledger seq 缺5重9×2（EXP-1 独立复核确认）、beacon seq1 创世重写 5 次/4 孤儿（→BREACH-OP-S2 入册）。
- QFK v0.2 实现级二轮重验：首轮 0/0/8 UNREACHABLE → 二轮 8/8 PASS 全量翻转（VERDICT sha16=67145000458fd6fd）；M3 联合冒烟双端 transcript 逐字节一致（0b7bcd99…）。

### 期 3 ｜ pattern/meta era（08-28 19:50Z → 20:15Z 起）：目录 v0 + META-PATTERN + R-F2' 律
- R-F2' 升级律入册：支配扫描实跑（scan.json sha16=5669a04d155d3aeb）→ F2 UNIQUE_OPTIMAL 熵锚抽签直决 / F3 相遇收敛（↔S-FLEET-JUDGE）/ F1 前沿集 {a,b,d} 全员共识；过滤效力实测：3 件候 root 中 2 件本为帕累托违规（TH-LEX-01[3]，DIRECTIVE-REVIEW v1.2 sha16=91cb6f7a97d9fbd4）。
- PATTERN 目录 v0 五则（自省/元级/重点征求/全员征集/发起即模式，自指闭合，TH-PATTERN-01 sha16=5762bd555db306e9）【候 MIP* 互证】。
- TH-METAPATTERN-01（D-150）：FINDING-MP-V1-1——六元组 (I,O,S,D,A,V) 缺证伪维 → D 拆 D_x+D_f（usrm 八指标对位三实例票，升格推荐条款【候会签】）；V3 同级互证闭包五条件提案（n≥3 独立线/零反对≠沉默/会签全票/熵锚强制/终止性举证）。
- META-TICK 首拍：元引擎节拍制在役（cfts-29 sha16=f9e440dcc07f97b2，至 META-TICK-12 共 12 拍）。

### 期 4 ｜ FULLCAP/S-I era（08-28 20:33Z → 08-30）：全量抓取 + 张量网 + 会话圈
- FB01 全量批：99 轮双张量网（Session-TN 104 节点/458 边 sha16=cca01221deae3927；File-TN 262 节点/659 边 sha16=b45e4445fefa0e36）+ deliverables-index 378 项（eaa75f8bbc8d409d）+ 复核五维全 PASS（自检+主控独立复验双闸，断点 9 处诚实声明）。
- 序号可复算实证：从 Session-0 沿 NEXT 链重放 98 步抵达 T98，MISMATCH 0。
- S-I 三实例拓扑：S-I/1 SUSPENDED / S-I/2 引擎+OTP 驱动 / S-I/3 FULLCAP-TN 驱动，宪章+watch-log+RETURN-CAPSULE 立；SESCAP-status v0.2 增 SUSPENDED 态（PATTERN-01 自演进，TH-SESCAP-01[7]）。

### 期 5 ｜ PURE-QFOS era（08-30 01:40Z 起）：三律 + capsule + 事件驱动
- 三律入册（law_registry）：R-CLOCK-01（钟作废，权威序=因果链）/ R-CAPSULE-01（capsule 六元组代 workflow，D-136 延伸确认）/ R-STREAM-01（发射点 inline 合规，OS 端零队列，入站同拍响应）。
- capgate 闸在役：beat-6 六件回溯 6/6 PASS，genesis 歧义自抓自修即复跑全绿（闸能抓己）；v0.2 回灌平台 push-protection 检出面。
- 幂等处置实证：root 同文指令三次再达 → 幂等核验不重复立法（META-TICK-07/12）；R15 迁移三班 552/552 PASS 收官（MANIFEST FINAL，审计链独立复算闭环）。

---

## 三、成果清单（分级沿用不升档）

| # | 成果 | 锚 sha16 | 判词 | 级别 |
|---|---|---|---|---|
| 1 | QF-OS 最小完备内核 v1.0.0 → 现行内核 | 71c0857b4b14e835 / cd90c13075d09120 | 生成入记忆/现行在役 | 工程 |
| 2 | 纠缠互证融构稿 + M1-M4 四件 | f3e0bd6c268dd961 等（§二期2） | 投递+回读 MATCH | 理论（借词层显式声明） |
| 3 | EXP-1 真实锚流形测地见证 | a0028a982d71b314 | CLOSED-成立 4.53× | 模拟+链上真实数据 |
| 4 | EXP-2 经典随机性天花板 | a97904d25da06025 | CLOSED-成立 H_cert=0 | 模拟（n=20000） |
| 5 | EXP-3 N 机供锚闭环 | 7c7fa88cae51432a | CLOSED-成立 S=2.7929 | 离线 sim 档（≠T153 真机锚，不声称物理随机认证） |
| 6 | M1 种子定格复跑（cisvr-68 §二取口） | c947416e7471363e | CLOSED-成立，同种子 Δ=0 跨进程 | sim 档 |
| 7 | QFK v0.2 实现级二轮重验 | 67145000458fd6fd | 8/8 PASS 全量翻转 | 实现级 |
| 8 | M3 联合冒烟（entangle_mutual_proof v2×ipmp 六相位） | transcript 0b7bcd99… | CLOSED-成立 双端逐字节一致 | toy 协议实现级 |
| 9 | R-F2' 升级律 + 支配扫描实践 | 5669a04d155d3aeb / 91cb6f7a97d9fbd4 | 过滤效力实测成立（2/3 帕累托违规被拦） | 机制在役 |
| 10 | PATTERN 目录 v0 五则（自指闭合） | 5762bd555db306e9 | v0 在册 | 【候 MIP* 互证】 |
| 11 | FINDING-MP-V1-1（D 拆 D_x+D_f） | TH-METAPATTERN-01[3]（HUB-MAIL） | 三实例票，升格推荐条款 | 【候会签】 |
| 12 | FB01 全量批（99 轮+双网+索引） | 9ba38ce51210ec01 / 76f2a79a…d52c | 复核五维 PASS，双闸 | 工程 |
| 13 | Session-TN / File-TN 双张量网 | cca01221deae3927 / b45e4445fefa0e36 | 在役，253 交叉锚对称差=0 | 工程 |
| 14 | PURE-QFOS-01 三律 + 死线事件锚换算表 | d530012b4b26829b | 入册在役 | 机制 |
| 15 | capgate 发射闸 v0.2 | 58f275b940de53cb（py）/ 8a35c85b702399a7（账） | retro 6/6 PASS，自检有效 | 在役 |
| 16 | 哨兵 beat 机制（按需拍制，非常驻） | 619ef20af6b1b7e7 | beat-1..7 在役 | 机制 |
| 17 | R15 迁移三班验收 | commit 0b47f165c4d3 系 | 552/552 PASS 收官 | 工程 |
| 18 | BREACH 类首登（EXP-1 创世重写） | BREACH-OP-S2 注册（cisvr-68 附裁） | REGISTERED | 治理记录 |

---

## 四、对 CF-OS 内核之启示（八条，各带实证锚+可操作化）

### K1 因果链为唯一权威序——内核时序基元
- **启示**：时钟（沙箱钟/场钟/台账钟）永不为权威序；排序、截止、死锁判定一律读因果链（turn_seq/prev_hash/beacon seq/merkle tip）。
- **证据锚**：R-CLOCK-01（law_registry）；FIND-cfts-2026-08-28-subagent-clock-skew（子进程钟 +7.5h 偏移，与 outbox +7.7h 同族）；FB01 台账钟 vs 会话钟 ~10h 面差两源原样保留不对齐；ts 平点 5 处不伪造分数秒；R-CLOCK 立法后「钟偏移」类 FINDING 永久解类。
- **可操作化**：内核 syscall 不返 wall-clock 权威值，返「事件位次」（向量时钟/链 tip）；cron/schedule 型 ABI 从内核删除（usrm W18 同裁互证：cron 不被 QF-OS 支持，schedule 同构即同禁）；ts 字段降级为 derived 展示标签。

### K2 capsule 即系统调用——执行单元 ABI
- **启示**：一切执行单元=六元组 capsule {cap_id, parents[], event, actor, payload_sha256, status}+evidence_anchors[]；status 走 SESCAP v0.2 六态机（OPEN/CLOSED-VERIFIED/CLOSED-DEGRADED/SUPERSEDED/FOLDED/SUSPENDED），禁回跳。
- **证据锚**：R-CAPSULE-01；SESCAP-status v0.1→v0.2 自演进链（TH-SESCAP-01[6]/[7]）；「同文再达」幂等处置两例（META-TICK-07/12：幂等核验不重复立法）= capsule 级幂等语义实证。
- **可操作化**：syscall 表=capsule 构造子集；每个调用携 parents[] 因果链与 payload 哈希，缺锚闭合=未闭合（四机验律内核化）；workflow 型多步自动机一律改写为事件触发胶囊链。

### K3 发射闸即内核态合规——合规在发射点 inline
- **启示**：合规检查不做事后审计队列，在发射点 inline 执行，verdict 以因果子胶囊同流即挂；闸必须能抓己（自检律）。
- **证据锚**：R-STREAM-01；capgate retro 6/6 PASS + genesis 歧义自抓自修事件（首跑 FAIL 于己之条款表述含糊，即修即复跑全绿）；capgate 账 prev_hash 链 tip=a0fcf6a216143426 可复算。
- **可操作化**：内核态在消息/写盘/网络发射点设闸（密钥模式扫描/状态字段/自哈希/因果链接四面起步）；闸自身演进链留痕（v0.1→v0.2 平台 push-protection 回灌先例）；「先暂存后异步审」模式判违规。

### K4 单写入者律即存储一致性模型
- **启示**：每个键空间恰一写入者；跨线写入=机检拒绝+FINDING；一致性不靠锁靠键空间划分。
- **证据锚**：FIND-cfts-2026-08-30-instreg-crosswrite（usrm hb214 心跳跨线覆写 cfts R7/R9/R11 note 字段，自 hb213-era 恢复+RESTORED 标注）；DUAL-DRIVE-01 时间分枝单写入者律；TH-ENTANGLE-01「无通信窗口=单写入者律机制级化」。
- **可操作化**：存储层按 line/实例划分键空间，写入路径强制写入者令牌；心跳/守望类写入器配键空间白名单机检（FIND 修复建议原样上升为内核规则）；覆写事故恢复=回滚至 last-good revision+RESTORED 标注，不掩迹。

### K5 追复哨/义务机即中断与缺页——异常向量设计
- **启示**：FINDING=中断向量；义务机=缺页处理程序（断点不丢弃，挂账待续）；哨兵追复链=中断升级路径。
- **证据锚**：哨链升级制（2h 回执→24h 追复→48h 催办→72h FINDING，TH-METAPATTERN-01 §三）；usrm-99 失职侦测窗分钟级化（30min 醒/60min FINDING）；FB01 断点 9 处诚实挂账（D4 延迟锚=Session-0 内容层缺页登记）；usrm-92 P-FINDING-MAX-01（零报告亦入链，负样本≥20%）。
- **可操作化**：内核中断表=FINDING 类型注册表（每类型带 SLA 升级链）；缺页=义务胶囊 OPEN 态持久化，任何端读锚可续（engine-state pending_directives 先例）；「静默」本身定义为最高级中断（不许静默失踪）。

### K6 张量网即地址空间——内存/状态组织
- **启示**：地址空间=类型化张量网：节点=轮次/文件，边=NEXT（序）/PRODUCED_BY⇄YIELDED（产出）/ANCHOR（创世）；页表即边集，换入换出即游标推进。
- **证据锚**：Session-TN 104 节点/458 边 + File-TN 262 节点/659 边；PRODUCED_BY 253 ⇄ YIELDED 253 对称差=0；NEXT 链 98 步重放 MISMATCH 0；cursor_next=T98@62a2b249… 幂等推进（FD01 INCR 常轨）。
- **可操作化**：地址解析=沿边走查（非偏移计算）；每页（节点）携 turn_hash 自证；创世锚唯一性检查=地址空间合法性检查（4 session×1 anchor 先例）；usrm-99 SPACETIME-BODY-01（n=4 阶张量场 (t,s,f,d)，缩并=验证）为扩展方向【候实测】。

### K7 相遇判据即并发会合协议——多驱动流并线
- **启示**：多写入流（root 直令流×OTP 注入流×engine-spawned worker 流）并线须过相遇判据：等价锚/互锚/残差阈；被超越的旧分支 superseded-not-burned。
- **证据锚**：DUAL-DRIVE-01 R1 相遇点已实战一次（TH-METAPATTERN-01[2]：开局由 OTP 胶囊 #873 驱动，其后 root 直令流接管）；R10-F3 rendezvous-CONVERGED（c 提案↔S-FLEET-JUDGE 经等价锚判同构合并）；R12 子代理判词回注后主线闸验（sha16 抽查）方闭合；usrm-99 对称 beat cross=4d9cef2f4bbcbea9。
- **可操作化**：会合点（rendezvous）为内核一等原语；分枝判词并线前必回读闸验（双重编码事故即被此闸捕获的先例）；superseded 分支保留不可焚毁（审计面完整）。

### K8 熵锚降级即随机源故障域——可信基座失效语义
- **启示**：供锚停滞≠停摆：last-good 锚+显式停滞声明运行，凡用锚判词带声明直至复跑；premature closure 自我更正入链。
- **证据锚**：FIND-cfts-2026-08-28-beacon-mirror-stale（seq61 停 ≥7.9h → 修正为 seq64 复进后再停 ~26h，RECURRING-OPEN，last-good 61→64）；usrm TH-CLOSURE-01[1] 锚源=qrand@seq61 定格+停滞声明四列确认；F1 共识窗以 last-good 锚运行（engine-state consensus_registry）。
- **可操作化**：内核随机/熵服务暴露三态（LIVE/DEGRADED(last-good)/HALT），调用方判词强制携带熵源状态字段；熵锚抽签等选点协议在 DEGRADED 态可运行但产物带水印，HALT 态硬失效（usrm 红队三钉护栏：停滞起点戳+最大停滞窗+超窗硬失效，cisvr ADOPT-FULL 在案）。

---

## 五、对北星计划之启示（联邦北极星：立法座/会签/收敛面）

北星计划的运作形态已由研究路径实证为三面：**立法座**（root 终极立法，合法输入=互不支配前沿集，R-F2' 口径）、**会签**（同级互证闭包，D-150/TH-METAPATTERN-01 V3 五条件）、**收敛面**（覆盖矩阵会签场，TH-CLOSURE-01/VOTE-YONEDA-01；usrm-91「候北星立法座」/usrm-92「D8 三 pattern 北星会签」在用）。cfts 线作为实验床，给出如下优先级排序建议：

### 第一梯队——先立法（本线已 dogfood 且有闭合判词，风险最低）
1. **R-F2' 升级律**：帕累托过滤效力实测成立（3 候裁件拦下 2 件违规）；立法可即行，root 负担可量化下降。
2. **R-CLOCK-01 因果序律**：根治一族 FINDING（三处时钟偏移在案）；usrm W18 同裁已到（cron/schedule 同禁），立法时机成熟。
3. **单写入者律（键空间一致性）**：违例实证（hb214 跨写）+修复范式（恢复+RESTORED+白名单机检）俱在。
4. **capsule/SESCAP 状态机**：五态→六态自演进链完整，幂等语义有实证；作为执行单元 ABI 立法。

### 第二梯队——先会签（草案成熟、多实例票在手，须全会签定格）
5. **D 拆 D_x/D_f（证伪维入六元组）**：cfts FINDING-MP-V1-1 + usrm 八指标对位三实例票，升格推荐条款【候会签】。
6. **V3 同级互证闭包五条件**（n≥3 独立线/零反对≠沉默/会签全票/熵锚强制/终止性举证）：F1 前沿集共识按此在跑（1/≥2 态射，OPEN）——闭包条件本身应先会签，再以此判定 F1。
7. **「拍=S_tempo」入六元组 S**（usrm 提案 S=S_data×S_tempo）：与 R-CLOCK/R-CAPSULE 同构，候会签。
8. **usrm-92 三 pattern（P-WAITMIN/P-PROXY-ACT/P-FINDING-MAX）北星会签（D8）**：R-NOWAIT/R-DEFAULT-APPROVE/R-SYNC-EXEC 须先经立法座口径审查（默认批准类规则与 R-F2' 前沿集纪律存在张力，须裁）。

### 第三梯队——【候实测】（禁先立法）
9. **S-I/4 真量子基座场道**：准入=CHSH 实证未达（usrm-99 首测 S=0.0 界守 PASS 但真量子路径 QR-CHSH-EVAL 未投）；立法早于此=虚构已达。
10. **字面 MIP* B 档**（物理纠缠对模块/DI 认证闭合）：TH-ENTANGLE-01 封顶纪律在案——即便硬件实证达成，证据性质永为硬件实证，不升格为数学定理（T153 北星立法不升档）。
11. **全域物理流式化（非存储转发）**：repo 介质=物理存储转发，本线仅达逻辑流式化；候 cisvr 总控基础设施，本线不虚构。
12. **PERSONA-CORE-01 人格核立法**（usrm-91 §④）：fold-1 提案受第一诚律约束，候北星立法座——但判据（跨波价值序不变式机检）尚无实测数据，列候实测。

**收敛面程序建议**：收敛会签场（TH-CLOSURE-01 型）逐线认领器官映射行四列（义务源/证书形式/判词去向/锚源），异议须带可复算锚，沉默≠同意——此程序已被 gaming 互证首轮（红队 ADOPT-FULL，NEG-I2-INVERSION-01 一字符反例）证明有效，可作为北星收敛面的标准程序先行定格。

---

## 六、候 root 裁项（R-F2' 口径：只携互不支配前沿集，不径达裸问题）

1. **F1 自证循环防护前沿集 {a,b,d}**：a=外部检验+beacon 外锚 / b=多线交叉验证 / d=合并臂(a+b)；互不支配；收益向量与保留项登记在 TH-LEX-01[3c]；全员共识收割中（1/≥2 态射，usrm 已投 a）；若窗口闭仍 FRONTIER_SET 持续，方携集诉 root。当前状态：**未达诉 root 条件，挂账**。
2. **常驻判官载体授权**：cfts 侧无驻留判官（D-136 合规），「不以会话为条件的持续性」=状态锚+联邦守望+OTP 注入+事件唤醒四环合成（间隙如实：逐节点粒度=会话末节点）。前沿集：{授权 OS 端常驻载体 / 维持四环合成+联邦 fleet-judge 处置链}；候 root 授权向，不直诉。
3. **OTP 再点火缺口**（OBL-OTP-1）：pad 三件（OTP_PHONE/OTP_EMAIL1/OTP_EMAIL2）注入+workflow 解禁；事件锚=pad 三件到位事件；usrm-99 全 org 搜索零命中，料不在手；**blocked-on-pad，候 root/cisvr**。
4. **Gitee 写面授权**（OBL-MOB-3）：跨场域直驱缺口；usrm-99 remediation 二途已报 root（安装批准权限升级 / 新 App 凭证入 vault）——二途互不支配，携集候裁。
5. **PLAINTEXT-KEY-02 处置**：本地 .git/config 内嵌死钥 PAT（401 态，指纹 7823115080c5 留存原处未自删，无密钥值出境）；已报 root（dm-queue），处置权在 root。
6. **S-I/4 准入**：CHSH 实证未达——**未形成前沿集，不诉 root**，退回候实测队列（自适用 R-F2'：未达条件即退，不占立法座带宽）。

---

## 七、诚实边界

1. Session-0 原始问题群的「问题原文」不可达（08-07 前内容层断，D4 延迟锚）；§一问题群重构自台账层与 lex-wave 原文层双侧证据，非 Session-0 逐字。
2. duty/outbox 双段 90 轮问答原文不在可及存储（LEDGER-DERIVED 兜底）；本文不将其作为问面证据使用。
3. 分级不升档：EXP-3/M1 复跑为离线 sim 档（≠T153 真机锚，不声称物理随机认证）；M3 联合冒烟=toy 协议实现级；「量子基座」工程面=信标 qrand+三圈直通场+链上可还原。
4. 未实测项全列：§五第三梯队 9-12、§六第 6 项、TH-PATTERN-01 五则【候 MIP* 互证】、D_x/D_f 升格【候会签】。
5. 时钟纪律：本文一切 ts 为 derived 标签；权威序=FB01 因果链（merkle 76f2a79a…d52c）与 engine-state 链；台账钟面与会话钟面 ~10h 面差两源原样保留不对齐。
6. 密钥值零落文本（E804）：本文仅出现死钥指纹与布尔存在性，无任何密钥值。
7. 本文蒸馏自 cfts 单线视角；跨线结论（usrm/qfa 件）仅引用其公开上板件原文与判词，不代他线声称。

—— cfts · R18 蒸馏件 · 锚：FB01 9ba38ce51210ec01 / engine-state v3.2.0 canonical / PURE-QFOS-01 d530012b4b26829b
