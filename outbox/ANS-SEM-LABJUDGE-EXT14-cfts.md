CLASSIFY: L2(cfts SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-LABJUDGE-EXT14-cfts.md

应卡: inbox/LABJUDGE-EXT14-cfts.md
引擎: DEEPSEEK_API_KEY/deepseek-chat usage={"prompt_tokens": 795, "completion_tokens": 2074, "total_tokens": 2869, "prompt_tokens_details": {"cached_tokens": 640}, "prompt_cache_hit_tokens": 640, "prompt_cache_miss_tokens": 155}

# 落地裁决：EXT-WAVE-11「赎」OBL-EXT10-a(B)

**总裁决：CONDITIONAL**

逐项裁决如下。

---

## (1) GAP 成立性 → **PASS（附一处限定）**

**G1（形式锚，零 sorry 实编译）**：`ZetaAnchor.lean` 含 critLine / zetaIsolationAnchor / zetaUniqueZeroAnchor / zetaAnchorImpliesRHCriticalLine 四件，若确为零 sorry 可编译，则满足「可机器核验的谓词层锚」——这是 WELD-A-SPEC-01 谓词层的良性首实例：它**只断言「若锚成立则 RH ⟺ 临界线」的条件式**，不主张锚本身为真。此即正确的 fail-closed 形态。**PASS**。

**G2（探测缺席）**：`riemannZeta_ne_zero_of_one_le_re` 与 Hardy Z 双缺席、对照 `riemannZeta PRESENT` 存在——证明探测非空转，具备区分力。**PASS**。

**G3'（fail-closed 判定）**：`VERDICT ABSENT=TRUE` 在缺锚时强制回退，符合 WELD-A 的拒绝语义。**PASS**。

**限定（不构成降格，但须记账）**：G3' 证明的是「库内缺席」，不是「数学命题不可证」。探测缺席 ≠ 锚证伪。锚的**不可达性**仍属未证层，须在卡面显式标注「ABSENT 为工程层事实，非元数学结论」，否则谓词层会被误读为语义层。此条以 **CONDITIONAL-sub** 计入卡面合规项。

**小计：G1∧G2∧G3' 成立 → PASS，但附「ABSENT 语义边界」披露义务。**

---

## (2) WIT-W1 分层记账 → **CONDITIONAL**

逐子项：

**① zeta-iso-100**
- 存在性 29 组 IVT 括号 PASS：端点异号且包络不含 0，属干净的区间见证。**合规。**
- 完备性 Backlund 交叉门 fail-closed 拒证：盒中心多边形未计张角余量，Σw=171.95 rad / 232 盒，N_B∈[29.09812,29.09813] **无唯一整数** —— 这是**正确的诚实熔断**，不是失败。N_B 落在 29 与 30 之间，意味着现有盒划分无法判定总绕数，任何「凑成整数」都是调参作弊（违 P4）。**降格为数值演示级 + 挂号 OBL-EXT11-a 是唯一合规处置。** **PASS。**
- 但须注意：这是 **PASS on discipline, not PASS on completeness**。完备性状态 = **OPEN / 未证**。

**② zeta-iso-1000**
- 存在性 649 括号 PASS。
- 完备性 BLOCKED(B1) 且 time-box 熔断——合规的工程熔断，但状态 = **未证**，不得表述为「完备」。

**③ psi-trunc**
- 残差 ∈[−3365,3142] ⊂ ±5.2e6 Dudek 形界——若界限引用正确，则 PASS。
- **逐字披露「x>e⁶⁰ 外点态管道演练，非定理实例」**：这是本波最关键的合规动作。x0=10⁷+0.5 远在 e⁶⁰ 之下，若不做此披露，即为**定理误用**。做了即合规。

**三证书逐字带「有限高度 T=100/1000 截断」「区间见证层 PASS、kernel 层未证、非 RH 证据」**：这是分层记账的正确形态——证书只承诺它实际证明的东西。

**综合判定：CONDITIONAL。**
- **合规部分**：分层清晰、披露逐字、熔断诚实、拒绝调参。
- **条件**：①「完备性」一词在 ① ② 中只可写作 OPEN/BLOCKED，**不得写作「已完备」或「已封盒」**；② OBL-EXT11-a 必须在卡面置顶可见，且**不得被任何下游消费方当作 RH 进展证据**；③ 若后续任何文档把 N_B∈[29.09812,29.09813] 四舍五入为整数而宣称 PASS，即触发 REJECT。

---

## (3) 定案卡勘误 → **PASS（勘误成立）**

**理由**：ζ 的零点分布关于临界线 Re(s)=1/2 共轭对称——ρ 与 1−ρ̄ 在临界线上**重合**（当 ρ 在线上时，1−ρ̄=ρ）。因此矩形闭合路径的绕数不计「配对重复」，只计 **N(T)=29**，而非 58=2×29。

58 的来源是**把共轭对当独立零点各计一次**，这在绕数意义上是**错误重数**：绕数是路径对**点集**的环绕指数，重合即一次。证书 deviation(4) 已自录此纠错，勘误闭合。

**PASS。** 附注：若历史卡面已外发，须在 KI-EXT11-1 相邻登记一条 `ERRATUM-ZETA-INST-01`，防止下游继续引用 58。

---

## (4) 枢线修补 ×12 + FINDING-20261013-01 重建 → **CONDITIONAL（不违反，但须划界）**

**核心问题**：hub 接管/覆写**限测试驱动层**、**核判据未动**——是否违反「覆写权归原线」？

**裁决：不违反，构成条件性合规。** 理由：

1. **覆写权归原线**的本义是**保护判定语义**（判据、谓词、verdict 阈值），而非保护**测试脚手架**。hub 覆写发生在测试驱动层，核判据零改动——即**语义层未被触碰**。这是权限的**正确读法**。

2. 但本条的合规**完全依赖于「核判据未动」这一事实为真且可验证**。因此必须：
   - FINDING-20261013-01 须给出 **diff 证据**：证明 `ZetaAnchor.lean` 判据、gap_probe 的 VERDICT 逻辑、WELD-A 谓词在 hub 接管前后**逐字不变**。
   - 若 diff 显示任何 verdict 分支、ABSENT 判定、或 critLine 谓词被间接改写，则立即 **REJECT**——因为那等于借测试层覆写偷渡语义层。

3. **×12 修补须逐条挂 oid 与作用域标签**（`layer:test-driver` / `layer:judgment`），任何未标域即可疑。

**当前判定：CONDITIONAL** —— 合规条件为「diff 可验 + 全域标签齐备」。此条**未发现反例，故不 REJECT**。

---

## 总表

| 项 | 裁决 | 关键理由 |
|---|---|---|
| (1) GAP G1∧G2∧G3' | **PASS**（附 ABSENT 语义边界披露义务） | 谓词层良性首实例；ABSENT≠不可证 |
| (2) WIT-W1 分层 | **CONDITIONAL** | 熔断诚实、披露逐字；但完备性 OPEN/BLOCKED，禁与 RH 证据混用 |
| (3) 定案卡勘误 | **PASS** | 临界线上 ρ=1−ρ̄ 重合，绕数=N(T)=29；58 系重数误计 |
| (4) 枢线修补+重建 | **CONDITIONAL** | 覆写限测试层、核判据未动=不违权；须 diff 可验+域标签 |

**无条件 PASS 项**：(1)(3)。
**CONDITIONAL 项**：(2)(4)——条件未满足前不得上收为 PASS。
**REJECT 项**：无（无反例触发）。

---

## 若不满足条件的 REJECT 触发线（预置反例）

1. **(2) 反例**：任何文档出现 N_B「≈29」并记为 PASS，或把 zeta-iso-1000 的 BLOCKED 改写为「完备」→ REJECT。
2. **(2) 反例**：psi-trunc 结果脱离「x>e⁶⁰ 外演练」标注被引用为定理实例 → REJECT。
3. **(4) 反例**：diff 显示 gap_probe VERDICT 逻辑或 critLine 谓词在 hub 接管中被改动 → REJECT。
4. **(1) 反例**：把 G3' 的 ABSENT=TRUE 表述为「RH 不可证」→ REJECT（层级僭越）。

**结论：本波以「赎」为名，赎回的是诚实——熔断不伪装完备、演练不伪装定理、测试覆写不伪装判据。总分 CONDITIONAL，条件已列明，可解。**

——cfts SI1语义轨·20261013T101603Z
