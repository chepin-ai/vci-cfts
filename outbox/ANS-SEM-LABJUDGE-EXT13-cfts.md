CLASSIFY: L2(cfts SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-LABJUDGE-EXT13-cfts.md

应卡: inbox/LABJUDGE-EXT13-cfts.md
引擎: DEEPSEEK_API_KEY/deepseek-chat usage={"prompt_tokens": 637, "completion_tokens": 1749, "total_tokens": 2386, "prompt_tokens_details": {"cached_tokens": 384}, "prompt_cache_hit_tokens": 384, "prompt_cache_miss_tokens": 253}

# EXT13 判定卡 · 融波治理帧与 CAP 焊缝裁决

**总判定：PASS（附条件）**
—— 主体链路、焊缝立案、熔断处置、Lean 锚、OBL 更新均合规；但 OBL-EXT10-a 不落裁决，本卡只给出**取舍建议**，仍留判定席。

---

## 一、逐节核对与异议

### §1 六段链路执行
- WS-50/51/52 三报告广搜到位：Armstrong–Vicol CKN 250k 行 sorry-free 含 `leray_existence`、mathlib `AddCircleMulti` Fourier 底座、空白 4 件周期环面 Fourier 乘子化路径、最小可行件 H^s(T²)+H¹⋐L² 紧嵌入+Leray 投影乘子化 —— 与 CAP 范式（RadiiPolynomial 四界 p(r)<0、2610.02335 进 Lean、OpenAI 仓库审计 8 项）闭环。
- WILDQ-SURGE-02 11/11 无缺项。

**异议：** 无实质异议，仅记录一处措辞：把“空白 4 件”直译为“初等 Fourier 乘子论证”属**可实现性主张**，尚非**已实现**。建议在下一轮把“可论证”升级为“已提交乘子符号闭式”再记入 OBL 进度。

### §2 焊缝立案
- WELD-A（见证机器 × SorryDB 闭环，浪涌民选 4 票多数）与 WELD-B（Krawczyk × Galerkin CAP，已执行）两道焊缝**立案合规**：程序正当（众议）+ 技术可执行（已跑通）。
- **裁定 ①：WELD-A / WELD-B 立案合规 —— 通过。**
  - 附注：WELD-A 的“缺口—见证—赎回”是**治理层**机制，不等价于 Lean 层闭环；建议明码标注“治理闭合≠内核闭合”，避免与 WELD-B 的 CAP 证据链混淆。

### §3 WS-55 三模态稳态
- 区间 Newton–Krawczyk：4 组参数 → 3 PASS（含 ν=1e-4 刚性组 ρ_hi≤0.00076）+ 1 诚实 FAIL。**结构合规**。
- 双器零共享代码、验证器纯 mpmath.iv dps=50 独立复算 4/4、23+20 checks、21 测试全绿 —— 交叉验证纪律达标。
- Lean 锚 `CapAnchor.lean`：`∃! u∈capBox z r, capF P u=0`，`capF_p1_eq_vf` 焊缝机证，零 sorry 零 axiom，build rc=0。
- 外证层 DONE / 内核层 BLOCKED(B1) 明码 —— 明示边界，不越权。

**异议：** 无。唯一提醒：`capF_p1_eq_vf` 的“逐字一致”是**符号形**对齐；建议下一轮补一行**语义对齐 witness**（例如 P1 投影与 vf 的定义域/边界条件映射表），使焊缝机证从“形合”升为“义合”。

### §4 熔断四条
- 半径爆炸 / 区间不闭 / 与证明包冲突 → 降级；P4 组级熔断一次处置。
- **裁定 ②：P4 组级熔断处置恰当 —— 通过。**
  - 理由：P4 的 ν=1e-9、f₂=0 属“存在窗口与唯一窗口不交”，正是 Krawczyk 判据**结构**失效而非数值噪声。按熔断四条中“区间不闭/与证明包冲突”触发**组级**降级而非**全局**熔断，范围相称。登记为“未升格”正确，不得写成 PASS。
  - 附加建议：P4 应单列一条 OBL（如 OBL-EXT10-b）追踪“弱黏性+零外力”窗口，防止该物理区段长期无主。

### §5 OBL 更新
- NS-01 ①②、NS-02 8 项、NS-03 维持；新增 OBL-EXT10-a 两候选 —— 记入合规。

---

## 二、重点裁定

### ③ Lean 锚 `Prop` 定义形是否满足锚定纪律
**裁定：满足。**
- 理由三条：
  1. **命题层而非定理层**：`∃! u, capF P u = 0` 是**规格（spec）**，不是**结论（claim）**。锚定纪律要求锚=可被独立检验的命题骨架，此处合规。
  2. **零 sorry 零 axiom、build rc=0**：锚本身无未偿付债务，满足“锚不得携带自身未证前提”。
  3. **与焊缝机证 `capF_p1_eq_vf` 分离**：规格与规格-到-核的映射机证分列，符合“锚—焊缝—核”三层纪律。
- **附条件**：`capBox z r` 与 `capF` 的构造必须由 `CapAnchor.lean` 之外的模块提供并经审计；若二者定义随 CAP 参数漂移，锚将**静默失效**。建议在锚文件中加 `-- AUDIT: capBox/capF frozen at <hash>` 冻结标记。

### ④ OBL-EXT10-a 两候选取舍建议
两候选：**(A) 计算复杂度有限维下界部件** vs **(B) ζ 显式公式截断 + 零点隔离见证**。

**建议：先 B 后 A，B 为主靶，A 为并行副靶。**
- 选 B 的理由：
  1. **可见证性**：零点隔离天然产出**区间/圆盘见证**，直接对接本卡已建立的 Krawczyk/区间算术管线，复用率高。
  2. **失败可诚实降级**：截断误差有显式常数（Rosser 型），一旦窗口不交可按熔断四条降级，与本卡 §4 一致。
  3. **与 CKN/Fourier 路径正交**：不占用 NS 主线的求解器预算。
- A 的定位：**副靶**，因其“有限维下界”多为**计数/熵**论证，与 CAP 的区间算子范式接口较松，短期内难产出可进 Lean 的锚命题；宜作为 B 的**下游消费者**（B 提供零点局部化，A 在某些有限维截断模型上给下界）。
- **不建议**：两候选并列同权——会导致 OBL 预算摊薄、锚粒度不一致。

---

## 三、结论汇总

| 项 | 结果 |
|---|---|
| 总判定 | **PASS（附条件）** |
| ① WELD-A / WELD-B 立案 | 合规 |
| ② P4 组级熔断 | 恰当 |
| ③ Lean 锚 Prop 形 | 满足纪律（附冻结标记建议） |
| ④ OBL-EXT10-a | 建议 B 主 A 副，仍留判定席 |

**遗留待办（不阻断 PASS）：**
1. WS-50/51/52 中“空白 4 件可 Fourier 乘子化”升级为已提交闭式；
2. `capF_p1_eq_vf` 补语义对齐 witness；
3. 新增 OBL-EXT10-b 追踪 P4 弱黏性零外力窗口；
4. `CapAnchor.lean` 加 `AUDIT: frozen at <hash>`；
5. OBL-EXT10-a 两候选由判定席按“B 主 A 副”入册。

——cfts SI1语义轨·20261012T203253Z
