CLASSIFY: L2(cfts SI1语义应答·vinf代铸轨SEMANTIC-RESPONDER-01·覆写权归原线)
# outbox/ANS-SEM-WILDQ-R26B-FIX-CFTS-01.md

应卡: inbox/WILDQ-R26B-FIX-CFTS-01.md
引擎: 〈RED〉/deepseek-chat usage={"prompt_tokens": 124, "completion_tokens": 1433, "total_tokens": 1557, "prompt_tokens_details": {"cached_tokens": 0}, "prompt_cache_hit_tokens": 0, "prompt_cache_miss_tokens": 124}

# 评审：`convert ... using 1` 在 mathlib rev 漂移下的脆弱性

先说明：我无法访问你具体的 PR/commit，以下是基于你描述的**结构性评审**，不针对具体行号。

---

## (1) `convert ... using 1` 生成目标的 rev 漂移是否为已知脆弱模式？

**是，属于 mathlib 长期承认的脆弱模式之一**，虽未必有单一 "issue 编号" 背书，但社区共识明确：

- `convert h using n` 的目标由 **elaborator 在运行时构造**，其形态取决于：
  - 当前 `simp`/`norm_cast` 默认引理集（会随 rev 变动）
  - `↑`/`Subtype.val`/`Nat.cast` 的 coercion 注册状态
  - `OfNat`/`Nat.cast`/`Coe` 的实例解析路径
  - reducibility hints（`@[reducible]` 增删）
- 你观察到的 `↑2 · id 包装 · 2-1 未求值` 正是典型的 **coercion 展开深度依赖 rev** 的症状：
  - 旧 rev 上 elaborator 可能停在 `(2:ℝ)` 的 `OfNat` 层
  - 新 rev 上因为 `Nat.cast` 的 simp 规则或 `push_cast` 触发点变化，多出一层 `id`/`↑` 未消解
- 后果：`rfl` 子弹级联（如 `· rfl` / `all_goals rfl`）依赖**字面同构**，一旦漂移即 fail，且报错信息通常指向"目标不匹配"，误导性极强。

**结论**：这不是偶发 bug，是 `convert` 的**语义契约**——它只保证"存在统一化"，不保证目标形态跨 rev 稳定。mathlib 有非成文惯例：**在 `convert` 后不应假设目标字面形态**。

---

## (2) 更稳健的替代方案

按稳健性从高到低：

### A. 直接 `HasDerivAt` 链式组合（最推荐）
```
have h1 : HasDerivAt f f' x := ...
have h2 : HasDerivAt (fun y => ...) ... x := ...
exact h1.comp x h2   -- 或 .const_mul / .mul_const / .neg 等组合子
```
- 优点：**不经过 tactic 目标构造**，类型由 term-level 组合子的签名钉死，跨 rev 稳定。
- 若原证明是"证某函数导数 = 表达式 → 用 convert 搬到另一形态"，通常可用 `.congr_of_eventuallyEq` / `HasDerivAt.congr` 显式改写，把形态对齐的负担从 elaborator 移到你的 term 上。

### B. `convert` + 显式中间 `have` 归一
若必须用 `convert`，把归一化**显式化**而非依赖子弹 `rfl`：
```
convert h using 1
· push_cast; ring        -- 而非 rfl
· simp only [Nat.cast_ofNat, ...]; rfl
```
即你当前的 `solve + simp/push_cast` 组合子方向正确。

### C. `refine ... ?_` 手工留洞
```
refine h.comp ?_ |>.congr ?_   -- 形态由 h 的类型决定
```
比 `convert` 更可控，因为 hole 的类型来自**已知类型**而非新构造。

### D. 避免 `using 1`，改用全 `convert` + `ring_nf`
`using 1` 把剩余目标交给默认 `rfl` 语义，正是脆弱点；`convert`（无 `using`）后统一 `all_goals simp only [...]; ring` 更稳，但代价是可读性。

**建议**：能改 A 就改 A；否则 B（你现在的方向）是可接受的工程折衷。

---

## (3) 修复件 proof-script 风格是否符合 mathlib 审稿标准？

`convert ... ; · solve [simp; push_cast; ring]` 这类组合子链，mathlib reviewer 的常见态度：

**可接受，但有条件：**

1. **`solve` 内引理集应显式**（`simp only [...]` 或至少 `push_cast` 限定），避免默认 `simp` 集随 rev 漂移——这恰恰是你正在修的同类问题，若修复件自身又依赖默认 `simp`，reviewer 会指出。
2. **`ring`/`push_cast` 顺序**应注释意图：是消 coercion 还是消算术？最好加 `-- normalize ↑2 - 1` 之类。
3. **长度**：单行 `solve` 可读性尚可；若 `solve [...]` 内超过 2–3 个 tactic，reviewer 常要求拆成 `· ...` 分步，便于 diff 定位未来再漂移。
4. **是否应加 `@[simp]` 归一引理**：若多处出现同类 `↑2 - 1` 未求值，reviewer 可能反过来建议**补一条 coercion simp 引理**，从根上消除漂移，而不是每处 `push_cast`。这是更"mathlib 味"的修法。

**红线**：`solve [simp]`（裸 `simp`）几乎必被要求改；`rfl` 作为子弹在 `convert using` 后会被标记为"脆弱"，你替换掉它是**正确的方向**。

---

## 总结建议

| 问题 | 结论 |
|---|---|
| (1) 是否已知脆弱 | 是，`convert using n` 目标形态跨 rev 不稳定是公认模式 |
| (2) 更稳健替代 | 优先 `HasDerivAt` term 组合子（`.comp`/`.congr`）；次选显式 `convert` + 限定 `simp only` |
| (3) 风格 | `solve + push_cast` 方向对；但需**限定引理集**，并考虑把重复归一提升为 `@[simp]` 引理 |

若你能贴出修复件 diff 与原始 `convert` 行，我可以给出更具体的替换 term-level 证明草案（例如把 `HasDerivAt` 链直接写成 `.comp` 组合），以及判断是否值得上游补 simp 引理。

——cfts SI1语义轨·20260930T014159Z
